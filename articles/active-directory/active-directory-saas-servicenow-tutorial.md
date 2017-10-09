---
title: "Tutorial: Integração do Azure Active Directory com o ServiceNow | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e ServiceNow e ServiceNow rápida."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: df6a07dd1aa437198fbdb9d0a04ea14f3a320249
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a>Tutorial: Integração do Azure Active Directory com o ServiceNow
Neste tutorial, saiba como toointegrate ServiceNow e ServiceNow Express com o Azure Active Directory (Azure AD).

Integrar o ServiceNow e ServiceNow Express com o Azure AD fornece-lhe Olá seguintes vantagens:

* Pode controlar no Azure AD que tenha acesso tooServiceNow e ServiceNow rápida
* Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooServiceNow e ServiceNow rápida (Single Sign-On) com as respetivas contas do Azure AD
* Pode gerir as contas numa localização central - Olá portal clássico do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos
tooconfigure integração do Azure AD com o ServiceNow e Express do ServiceNow, terá de Olá seguintes itens:

* Uma subscrição do Azure AD
* Para o ServiceNow, uma instância ou o inquilino do ServiceNow, versão Calgary ou superior
* Para expressas ServiceNow, uma instância do ServiceNow rápida, versão Helsinki ou superior
* inquilino de ServiceNow Olá tem de ter Olá [vários fornecedor único início de sessão no plug-in](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) ativada. Isto pode ser feito [submeter um pedido de serviço](https://hi.service-now.com). 

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.
> 
> 

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

* Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.
* Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. A adição de ServiceNow de galeria Olá
2. Configurar e testar o Azure AD de sessão único-ServiceNow ou ServiceNow rápida

## <a name="adding-servicenow-from-hello-gallery"></a>A adição de ServiceNow de galeria Olá
tooconfigure Olá integração do ServiceNow ou ServiceNow Express com o Azure AD, é necessário tooadd ServiceNow Olá Galeria tooyour na lista de aplicações SaaS geridas. 

**tooadd ServiceNow da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá **portal clássico do Azure**, no painel de navegação esquerdo de Olá, clique em **do Active Directory**. 
   
    ![Active Directory][1]
2. De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.
3. Clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.
   
    ![Aplicações][2]
4. Clique em **adicionar** em Olá parte inferior da página Olá.
   
    ![Aplicações][3]
5. No Olá **que itens pretende toodo** caixa de diálogo, clique em **adicionar uma aplicação na Galeria de Olá**.
   
    ![Aplicações][4]
6. Na caixa de pesquisa de Olá, escreva **ServiceNow**.
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. No painel de resultados de Olá, selecione **ServiceNow**e, em seguida, clique em **concluída** aplicação de Olá tooadd.
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configura e teste do Azure AD-início de sessão único com ServiceNow ou ServiceNow rápida com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá ServiceNow é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá ServiceNow tem toobe estabelecida.
Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no ServiceNow. tooconfigure e teste do Azure AD-início de sessão único com ServiceNow, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On para ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Configurar o Azure AD Single Sign-On para ServiceNow rápida](#configuring-azure-ad-single-sign-on-for-servicenow-express)**  -tooenable sua toouse utilizadores esta funcionalidade.
3. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
4. **[Criar um utilizador de teste do ServiceNow](#creating-a-servicenow-test-user)**  -toohave um homólogo de Britta Simon no ServiceNow é-lhe representação toohello ligado do Azure AD.
5. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
6. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

> [!NOTE]
> Se quiser tooconfigure ServiceNow omita o passo 2. Da mesma forma, se quiser tooconfigure ServiceNow rápida omita passo 1.
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a>Configurar o Azure AD início de sessão único para o ServiceNow
1. No portal clássico do Azure AD de Olá, no Olá **ServiceNow** página de integração de aplicações, clique em **configurar o início de sessão único** tooopen Olá **configurar início de sessão único** caixa de diálogo .
   
    ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC749323.png "configurar o início de sessão único")

2. No Olá **como seria, como os utilizadores toosign no tooServiceNow** página, selecione **Microsoft Azure AD Single Sign-On**e, em seguida, clique em **seguinte**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC749324.png "configurar o início de sessão único")

3. No Olá **configurar definições de aplicação** página, execute Olá os seguintes passos:
   
    ![Configurar o URL da aplicação](./media/active-directory-saas-servicenow-tutorial/IC769497.png "configurar o URL da aplicação")
   
    a. no Olá **ServiceNow no URL sessão** caixa de texto, escreva o seu URL utilizado pela sua aplicação de ServiceNow utilizadores tooyour toosign-na seguir o padrão de Olá: `https://<instance-name>.service-now.com`.
   
    b. No Olá **identificador** caixa de texto, escreva o seu URL utilizado pela sua aplicação de ServiceNow utilizadores tooyour toosign-na seguir o padrão de Olá: `https://<instance-name>.service-now.com`.
   
    c. Clique em **Seguinte**

4. toohave do Azure AD automaticamente configurar ServiceNow para autenticação baseada em SAML, introduza o nome da instância de ServiceNow, nome de utilizador de admin e palavra-passe de administrador no Olá **automática configurar o início de sessão único** formam e clique em  *Configurar*. Tenha em atenção que nome de utilizador de admin Olá fornecido tem de ter Olá **security_admin** função atribuída em ServiceNow para este toowork. Caso contrário, toomanually configurar ServiceNow toouse do Azure AD como um fornecedor de identidade, clique em **configurar manualmente a aplicação Olá para o início de sessão único**, em seguida, clique em **seguinte** e Olá concluída passos seguintes.
   
    ![Configurar o URL da aplicação](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "configurar o URL da aplicação")

5. No Olá **configurar o início de sessão único em ServiceNow** página, clique em **Transferir certificado**, guarde o ficheiro de certificado Olá localmente no seu computador.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC749325.png "configurar o início de sessão único")

6. Início de sessão tooyour ServiceNow aplicação como um administrador.

7. Ativar Olá *integração - vários único início de sessão instalador de fornecedor* Plug-in seguindo Olá passos seguintes:
   
    a. No painel de navegação de Olá no lado esquerdo Olá, aceda demasiado**definição de sistema** secção e, em seguida, clique em **plug-ins**.
   
    ![Configurar o URL da aplicação](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "ativar Plug-in")
   
    b. Procurar *integração - vários único início de sessão instalador de fornecedor*.
   
    ![Configurar o URL da aplicação](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "ativar Plug-in")
   
    c. Selecione o plug-in de Olá. Rigth clique e selecione **ativar/atualização**.
   
    d. Clique em Olá **ativar** botão.

8. No painel de navegação de Olá no lado esquerdo Olá, clique em **propriedades**.  
   
    ![Configurar o URL da aplicação](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "configurar o URL da aplicação")

9. No Olá **várias propriedades do fornecedor de SSO** caixa de diálogo, efetuar Olá os seguintes passos:
   
    ![Configurar o URL da aplicação](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "configurar o URL da aplicação")
   
    a. Como **ativar o fornecedor de várias SSO**, selecione **Sim**.
   
    b. Como **ativar registo de depuração obteve Olá fornecedor de várias integração SSO**, selecione **Sim**.
   
    c. No **campo Olá utilizador Olá tabela que...**  caixa de texto, tipo **user_name**.
   
    d. Clique em **Guardar**.

10. No painel de navegação de Olá no lado esquerdo Olá, clique em **certificados x509**.
    
     ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "configurar o início de sessão único")

11. No Olá **certificados x. 509** caixa de diálogo, clique em **novo**.
    
     ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "configurar o início de sessão único")

12. No Olá **certificados x. 509** caixa de diálogo, efetuar Olá os seguintes passos:
    
     ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "configurar o início de sessão único")
    
     a. Clique em **Novo**.
    
     b. No Olá **nome** caixa de texto, escreva um nome para a sua configuração (por ex.: **TestSAML2.0**).
    
     c. Selecione **Active Directory**.
    
     d. Como **formato**, selecione **PEM**.
    
     e. Como **tipo**, selecione **confiar o arquivo de certificados**.
    
     f. Abra o certificado codificado em Base64 no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência e, em seguida, cole-toohello **PEM certificado** caixa de texto.
    
     g. Clique em **atualização**.

13. No painel de navegação de Olá no lado esquerdo Olá, clique em **fornecedores de identidade**.
    
     ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "configurar o início de sessão único")

14. No Olá **fornecedores de identidade** caixa de diálogo, clique em **novo**:
    
     ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "configurar o início de sessão único")

15. No Olá **fornecedores de identidade** caixa de diálogo, clique em **SAML2 atualização1?**:
    
     ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "configurar o início de sessão único")

16. Na caixa de diálogo de propriedades de atualização1 SAML2 Olá, execute Olá os seguintes passos:
    
     ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "configurar o início de sessão único")

    a. no Olá **nome** caixa de texto, escreva um nome para a sua configuração (por ex.: **SAML 2.0**).

    b. No Olá **campo utilizador** caixa de texto, tipo **e-mail** ou **user_name**, consoante o campo que é utilizado toouniquely identificar os utilizadores na sua implementação do ServiceNow. 

    > [!NOTE] 
    > Pode tooemit configue do Azure AD ou ID de utilizador Olá do Azure AD (nome principal de utilizador) ou Olá endereço de correio eletrónico como Olá Identificador exclusivo no token SAML Olá por vai toohello **ServiceNow > atributos > Single Sign-On** secção Olá portal clássico do Azure e mapeamento Olá pretendido campo toohello **nameidentifier** atributo. valor de Olá armazenado para o atributo selecionado Olá no Azure AD (por exemplo, nome principal de utilizador) tem de corresponder ao valor de Olá armazenado no ServiceNow para o campo de Olá introduzido (por exemplo, user_name)

    c. No portal clássico do Azure AD de Olá, copie Olá **ID do fornecedor de identidade** valor e, em seguida, cole-o Olá **URL do fornecedor de identidade** caixa de texto.

    d. No portal clássico do Azure AD de Olá, copie Olá **URL de pedido de autenticação** valor e, em seguida, cole-o Olá **AuthnRequest do fornecedor de identidade** caixa de texto.

    e. No portal clássico do Azure AD de Olá, copie Olá **único URL de serviço Sign-Out** valor e, em seguida, cole-o Olá **SingleLogoutRequest do fornecedor de identidade** caixa de texto.

    f. No Olá **home page do ServiceNow** caixa de texto, tipo Olá URL da sua home page de instância de ServiceNow.

    > [!NOTE] 
    > Home page de instância do ServiceNow Olá é uma concatenação do seu **ServieNow URL de inquilino** e **/navpage.do** (por ex.:`https://fabrikam.service-now.com/navpage.do`).

    g. No Olá **ID de entidade / emissor** caixa de texto, tipo Olá URL do seu inquilino do ServiceNow.

    h. No Olá **URL público-alvo** caixa de texto, tipo Olá URL do seu inquilino do ServiceNow. 

    posso. No Olá **protocolo do enlace para Olá do IDP SingleLogoutRequest** caixa de texto, tipo **urn: oasis: os nomes: tc: SAML:2.0:bindings:HTTP-redirecionar**.

    j. Na caixa de texto de política de NameID Olá, escreva **urn: oasis: os nomes: tc: SAML:1.1:nameid-formato: não especificado**.

    k. Anular seleção de **criar um AuthnContextClass**.

    l. No Olá **AuthnContextClassRef método**, tipo `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`. Só é necessária se estiverem organização apenas de nuvem. Se estiver a utilizar no local ADFS ou MFA para a autenticação, em seguida, não deve configurar este valor. 

    m. No **desfasamento de relógio** caixa de texto, tipo **60**.

    n. Como **início de sessão único no Script**, selecione **MultiSSO_SAML2_Update1**.

    Nã. Como **x509 certificado**, selecione o certificado de Olá que criou no passo anterior Olá.

    p. Clique em **submeter**. 

1. No portal clássico do Azure AD de Olá, selecione a confirmação de configuração de início de sessão único Olá e, em seguida, clique em **seguinte**. 
   
    ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "configurar o início de sessão único")

2. No Olá **único início de sessão confirmação** página, clique em **concluída**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "configurar o início de sessão único")

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a>Configurar o Azure AD início de sessão único para ServiceNow rápida
1. No portal clássico do Azure AD de Olá, no Olá **ServiceNow** página de integração de aplicações, clique em **configurar o início de sessão único** tooopen Olá **configurar início de sessão único** caixa de diálogo .
   
    ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC749323.png "configurar o início de sessão único")

2. No Olá **como seria, como os utilizadores toosign no tooServiceNow** página, selecione **Microsoft Azure AD Single Sign-On**e, em seguida, clique em **seguinte**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC749324.png "configurar o início de sessão único")

3. No Olá **configurar definições de aplicação** página, execute Olá os seguintes passos:
   
    ![Configurar o URL da aplicação](./media/active-directory-saas-servicenow-tutorial/IC769497.png "configurar o URL da aplicação")
   
    a. no Olá **ServiceNow no URL sessão** caixa de texto, escreva o seu URL utilizado pela sua aplicação de ServiceNow utilizadores tooyour toosign-na seguir o padrão de Olá: `https://<instance-name>.service-now.com`.
   
    b. No Olá **URL do emissor** caixa de texto, escreva o seu URL utilizado pela sua aplicação de ServiceNow utilizadores tooyour toosign-na seguir o padrão de Olá `https://<instance-name>.service-now.com`.
   
    c. Clique em **Seguinte**

4. Clique em **configurar manualmente a aplicação Olá para o início de sessão único**, em seguida, clique em **seguinte** e Olá concluir os passos seguintes.
   
    ![Configurar o URL da aplicação](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "configurar o URL da aplicação")

5. No Olá **configurar o início de sessão único em ServiceNow** página, clique em **Transferir certificado**, guarde o ficheiro de certificado Olá localmente no seu computador e, em seguida, clique em **seguinte**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC749325.png "configurar o início de sessão único")

6. Início de sessão tooyour ServiceNow rápida aplicação como um administrador.

7. No painel de navegação de Olá no lado esquerdo Olá, clique em **Single Sign-On**.  
   
    ![Configurar o URL da aplicação](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "configurar o URL da aplicação")

8. No Olá **Single Sign-On** caixa de diálogo, clique em Olá configuração no ícone no limite superior de Olá direita e defina hello seguintes propriedades:
   
    ![Configurar o URL da aplicação](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "configurar o URL da aplicação")
   
    a. Ativar/desativar **ativar o fornecedor de várias SSO** toohello direito.
   
    b. Ativar/desativar **depuração de ativar o registo para Olá fornecedor de várias integração SSO** toohello direito.
   
    c. No **campo Olá utilizador Olá tabela que...**  caixa de texto, tipo **user_name**.
9. No Olá **Single Sign-On** caixa de diálogo, clique em **adicionar novo certificado**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "configurar o início de sessão único")
10. No Olá **certificados x. 509** caixa de diálogo, efetuar Olá os seguintes passos:
    
    ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "configurar o início de sessão único")
    
    a. No Olá **nome** caixa de texto, escreva um nome para a sua configuração (por ex.: **TestSAML2.0**).
    
    b. Selecione **Active Directory**.
    
    c. Como **formato**, selecione **PEM**.
    
    d. Como **tipo**, selecione **confiar o arquivo de certificados**.
    
    e. Crie um ficheiro de codificado em Base64 a partir do seu certificado transferido.
    
    > [!NOTE]
    > Para obter mais detalhes, consulte [como tooconvert um binário de certificado para um ficheiro de texto](http://youtu.be/PlgrzUZ-Y1o).
    > 
    > 
    
    f. Abra o certificado codificado em Base64 no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência e, em seguida, cole-toohello **PEM certificado** caixa de texto.
    
    g. Clique em **atualização**.
11. No Olá **Single Sign-On** caixa de diálogo, clique em **Adicionar nova IdP**.
    
    ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "configurar o início de sessão único")
12. No Olá **adicionar novo fornecedor de identidade** caixa de diálogo, em **configurar o fornecedor de identidade**, efetuar Olá os seguintes passos:
    
    ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "configurar o início de sessão único")

    a. no Olá **nome** caixa de texto, escreva um nome para a sua configuração (por ex.: **SAML 2.0**).

    b. No portal clássico do Azure AD de Olá, copie Olá **ID do fornecedor de identidade** valor e, em seguida, cole-o Olá **URL do fornecedor de identidade** caixa de texto.

    c. No portal clássico do Azure AD de Olá, copie Olá **URL de pedido de autenticação** valor e, em seguida, cole-o Olá **AuthnRequest do fornecedor de identidade** caixa de texto.

    d. No portal clássico do Azure AD de Olá, copie Olá **único URL de serviço Sign-Out** valor e, em seguida, cole-o Olá **SingleLogoutRequest do fornecedor de identidade** caixa de texto.

    e. Como **certificado do fornecedor de identidade**, selecione o certificado de Olá que criou no passo anterior Olá.


1. Clique em **definições avançadas**e, em **propriedades do fornecedor de identidade adicionais**, efetuar Olá os seguintes passos:
   
    ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "configurar o início de sessão único")
   
    a. No Olá **protocolo do enlace para Olá do IDP SingleLogoutRequest** caixa de texto, tipo **urn: oasis: os nomes: tc: SAML:2.0:bindings:HTTP-redirecionar**.
   
    b. No Olá **NameID política** caixa de texto, tipo **urn: oasis: os nomes: tc: SAML:1.1:nameid-formato: não especificado**.    
   
    c. No Olá **AuthnContextClassRef método**, tipo **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.
   
    d. Anular seleção de **criar um AuthnContextClass**.

2. Em **propriedades adicionais de fornecedor de serviço**, efetuar Olá os seguintes passos:
   
    ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "configurar o início de sessão único")
   
    a. No Olá **home page do ServiceNow** caixa de texto, tipo Olá URL da sua home page de instância de ServiceNow.
   
    > [!NOTE]
    > Home page de instância do ServiceNow Olá é uma concatenação do seu **ServieNow URL de inquilino** e **/navpage.do** (por ex.: `https://fabrikam.service-now.com/navpage.do`).
    > 
    > 
   
    b. No Olá **ID de entidade / emissor** caixa de texto, tipo Olá URL do seu inquilino do ServiceNow.
   
    c. No Olá **URI de audiência** caixa de texto, tipo Olá URL do seu inquilino do ServiceNow. 
   
    d. No **desfasamento de relógio** caixa de texto, tipo **60**.
   
    e. No Olá **campo utilizador** caixa de texto, tipo **e-mail** ou **user_name**, consoante o campo que é utilizado toouniquely identificar os utilizadores na sua implementação do ServiceNow.
   
    > [!NOTE]
    > Pode tooemit configue do Azure AD ou ID de utilizador Olá do Azure AD (nome principal de utilizador) ou Olá endereço de correio eletrónico como Olá Identificador exclusivo no token SAML Olá por vai toohello **ServiceNow > atributos > Single Sign-On** secção Olá portal clássico do Azure e mapeamento Olá pretendido campo toohello **nameidentifier** atributo. valor de Olá armazenado para o atributo selecionado Olá no Azure AD (por exemplo, nome principal de utilizador) tem de corresponder ao valor de Olá armazenado no ServiceNow para o campo de Olá introduzido (por exemplo, user_name)
    > 
    > 
   
    f. Clique em **Guardar**. 

3. No portal clássico do Azure AD de Olá, selecione a confirmação de configuração de início de sessão único Olá e, em seguida, clique em **seguinte**. 
   
    ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "configurar o início de sessão único")

4. No Olá **único início de sessão confirmação** página, clique em **concluída**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "configurar o início de sessão único")

## <a name="configuring-user-provisioning"></a>Configurar o aprovisionamento de utilizadores
o objetivo desta secção Olá é toooutline como tooenable aprovisionamento de utilizadores do utilizador do Active Directory tooServiceNow de contas.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure aprovisionamento de utilizadores, execute Olá os seguintes passos:
1. No Olá Azure Management portal clássico, no Olá **ServiceNow** página de integração de aplicações, clique em **configurar o aprovisionamento de utilizadores**. 
   
    ![Aprovisionamento de utilizadores](./media/active-directory-saas-servicenow-tutorial/IC769498.png "aprovisionamento de utilizadores")

2. No Olá **introduza aprovisionamento de utilizadores automática do ServiceNow credenciais tooenable** , indique Olá seguintes definições de configuração:
   
     a. No Olá **nome da instância do ServiceNow** caixa de texto, o nome de instância do tipo Olá ServiceNow.
   
     b. No Olá **nome de utilizador de Admin do ServiceNow** caixa de texto, nome do tipo Olá de Olá conta de administrador do ServiceNow.
   
     c. No Olá **palavra-passe de administrador de ServiceNow** caixa de texto, tipo Olá palavra-passe desta conta.
   
     d. Clique em **validar** tooverify a configuração.
   
     e. Clique em Olá **seguinte** Olá do botão tooopen **passos** página.
   
     f. Se pretender que tooprovision todos os utilizadores toothis aplicação, selecione "**aprovisionar automaticamente todas as contas de utilizador na aplicação do Olá diretório toothis**". 
   
    ![Próximos passos](./media/active-directory-saas-servicenow-tutorial/IC698804.png "próximos passos")
   
     g. No Olá **passos** página, clique em **concluída** toosave a configuração.

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
Nesta secção, vai criar um utilizador de teste no portal clássico Olá chamado Britta Simon.

![Criar utilizador do Azure AD][20]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal clássico do Azure**, no painel de navegação esquerdo de Olá, clique em **do Active Directory**.
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.

3. lista de Olá toodisplay de utilizadores, no menu de Olá na parte superior do Olá, clique em **utilizadores**.
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. Olá tooopen **adicionar utilizador** caixa de diálogo, na barra de ferramentas de Olá na parte inferior do Olá, clique em **adicionar utilizador**.
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. No Olá **diga-nos informações sobre este utilizador** diálogo página, execute Olá os seguintes passos:
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    a. Como tipo de utilizador, selecione o novo utilizador na sua organização.
   
    b. No nome de utilizador de Olá **textbox**, tipo **BrittaSimon**.
   
    c. Clique em **Seguinte**.

6. No Olá **perfil de utilizador** diálogo página, execute Olá os seguintes passos:
   
   ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   a. No Olá **nome próprio** caixa de texto, tipo **Britta**.  
   
   b. No Olá **Apelido** caixa de texto, tipo, **Simon**.
   
   c. No Olá **nome a apresentar** caixa de texto, tipo **Britta Simon**.
   
   d. No Olá **função** lista, selecione **utilizador**.
   
   e. Clique em **Seguinte**.

7. No Olá **Get palavra-passe temporária** página da caixa de diálogo, clique em **criar**.
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. No Olá **Get palavra-passe temporária** diálogo página, execute Olá os seguintes passos:
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    a. Anote o valor Olá Olá **nova palavra-passe**.
   
    b. Clique em **Concluído**.   

### <a name="creating-a-servicenow-test-user"></a>Criar um utilizador de teste do ServiceNow
Nesta secção, vai criar um utilizador chamado Britta Simon ServiceNow. Nesta secção, vai criar um utilizador chamado Britta Simon ServiceNow. Se não souber como tooadd no seu ServiceNow ou ServiceNow rápida da conta de utilizador, contacte a equipa de suporte do ServiceNow.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD
Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo utras tooServiceNow de acesso.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooServiceNow, execute Olá os seguintes passos:**

1. No portal clássico Olá, clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.
   
    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **ServiceNow**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. No menu de Olá na parte superior do Olá, clique em **utilizadores**.
   
    ![Atribua o utilizador][203] 

4. Na lista de todos os utilizadores de Olá, selecione **Britta Simon**.

5. Na barra de ferramentas Olá na parte inferior de Olá, clique em **atribuir**.
   
    ![Atribua o utilizador][205]

### <a name="testing-single-sign-on"></a>Teste o início de sessão único
o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.

Ao clicar em mosaico de ServiceNow Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour ServiceNow aplicação.

## <a name="additional-resources"></a>Recursos adicionais
* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
