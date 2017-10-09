---
title: "Tutorial: Integração do Azure Active Directory com TimeOffManager | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e TimeOffManager."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: c871257bfb49883e31b1c4860a9d7faa70e9ab48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a>Tutorial: Integração do Azure Active Directory com TimeOffManager

Neste tutorial, saiba como toointegrate TimeOffManager com o Azure Active Directory (Azure AD).

Integrar TimeOffManager com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooTimeOffManager
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooTimeOffManager (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com TimeOffManager tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um TimeOffManager-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar TimeOffManager da Galeria de Olá
2. Configurar e testar o Azure AD-início de sessão único

## <a name="add-timeoffmanager-from-hello-gallery"></a>Adicionar TimeOffManager da Galeria de Olá
tooconfigure Olá integração de TimeOffManager com o Azure AD, é necessário tooadd TimeOffManager Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd TimeOffManager da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **TimeOffManager**, selecione **TimeOffManager** do painel de resultados e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Adicionar a partir da Galeria](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD-início de sessão único
Nesta secção, configure e teste do Azure AD-início de sessão único com TimeOffManager com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá TimeOffManager é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá TimeOffManager tem toobe estabelecida.

No TimeOffManager, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com TimeOffManager, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste TimeOffManager](#create-a-timeoffmanager-test-user)**  -toohave um homólogo de Britta Simon no TimeOffManager é toohello ligado do Azure AD de representação do utilizador.
4. **[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação TimeOffManager.

**tooconfigure do Azure AD-início de sessão único com TimeOffManager, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **TimeOffManager** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![SAML com base em início de sessão](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. No Olá **TimeOffManager domínio e os URLs** secção, execute o seguinte Olá:

     ![Secção TimeOffManager domínio e os URLs](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`

    > [!NOTE] 
    > Este valor não é real. Atualize este valor com o URL de resposta real Olá. Pode obter este valor de **início de sessão único na página Definições** que é explicado mais tarde no tutorial Olá ou contacte [equipa de suporte de TimeOffManager](http://www.timeoffmanager.com/contact-us.aspx).
 
4. No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![Secção de certificado de assinatura de SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. o objetivo desta secção Olá é toooutline como tooenable utilizadores tooauthenticate tooTimeOffManger à respetiva conta no Azure AD com Federação com base no protocolo SAML Olá.
    
    A aplicação de TimeOffManger espera asserções de SAML Olá num formato específico, que requer tooadd atributo personalizado mapeamentos tooyour configuração SAML do token de atributos. Olá seguinte captura de ecrã mostra um exemplo para este.

    ![atributos de token SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "atributos token saml")
    
    | Nome do atributo | Valor do atributo |
    | --- | --- |
    | nome próprio |User.givenName |
    | Apelido |User.Surname |
    | E-mail |User.Mail |
    
    a.  Para cada linha de dados na tabela de Olá acima, clique em **adicionar o atributo de utilizador**.
    
    ![atributos de token SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "atributos token saml")
    
    ![atributos de token SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "atributos token saml")
    
    b.  No Olá **nome de atributo** caixa de texto, nome de atributo do tipo Olá mostrado para essa linha.
    
    c.  No Olá **valor do atributo** caixa de texto, o valor do atributo Olá selecione mostrado para essa linha.
    
    d.  Clique em **OK**.
    
6. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. No Olá **TimeOffManager configuração** secção, clique em **configurar TimeOffManager** tooopen **configurar início de sessão** janela. Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Secção de configuração de TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. Numa janela do browser web diferente, inicie sessão no site da sua empresa TimeOffManager como administrador.

9. Aceda demasiado**conta \> opções de conta \> as definições de início de sessão único**.
   
   ![Single Sign-On definições](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "único as definições de início de sessão")
7. No Olá **as definições de início de sessão único** secção, execute Olá os seguintes passos:
   
   ![Single Sign-On definições](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "único as definições de início de sessão")
   
   a. Abra o seu certificado codificado base-64 no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência e, em seguida, cole Olá certificados inteira no **certificado x. 509** caixa de texto.
   
   b. No **Idp emissor** caixa de texto, colar Olá valor **ID de entidade de SAML** que copiou do portal do Azure.
   
   c. No **URL de ponto final do IdP** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML** que copiou do portal do Azure.
   
   d. Como **impor SAML**, selecione **não**.
   
   e. Como **Auto-criar utilizadores**, selecione **Sim**.
   
   f. No **URL de fim de sessão** caixa de texto, colar Olá valor **Sign-Out URL** que copiou do portal do Azure.
   
   g. Clique em **guardar alterações**.

11. No **as definições de início de sessão único** página cópia Olá valor **asserção URL do serviço de consumidor** e colá-lo na Olá **URL de resposta** caixa de texto em **TimeOffManager Domínios e URLs** secção no portal do Azure. 

      ![Single Sign-On definições](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "único as definições de início de sessão")

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Utilizadores e grupos--> todos os utilizadores](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Botão Adicionar](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Página de caixa de diálogo de utilizador](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="create-a-timeoffmanager-test-user"></a>Criar um utilizador de teste TimeOffManager

Na ordem tooenable do Azure AD os utilizadores toolog para TimeOffManager, têm de ser tooTimeOffManager aprovisionado.  

TimeOffManager apenas suporta o aprovisionamento de utilizadores do tempo. Não há nenhum item de ação para si.  

são adicionados automaticamente utilizadores de Olá durante Olá primeiro início de sessão utilizando o início de sessão único em.

>[!NOTE]
>Pode utilizar quaisquer outras TimeOffManager utilizador conta criação ferramentas ou APIs fornecidas pelo TimeOffManager tooprovision contas de utilizador do Azure AD.
> 

### <a name="assign-hello-azure-ad-test-user"></a>Atribua o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooTimeOffManager.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooTimeOffManager, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **TimeOffManager**.

    ![TimeOffManager na lista de aplicações](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar em mosaico de TimeOffManager Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour TimeOffManager aplicação. Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

