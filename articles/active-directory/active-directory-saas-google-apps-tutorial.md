---
title: "Tutorial: Integração do Azure Active Directory com o Google Apps no Azure | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e o Google Apps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2093b5ab605ec0d7bbefe7a78e1eede34d756f53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a>Tutorial: Integração do Azure Active Directory com o Google Apps

Neste tutorial, saiba como toointegrate Google Apps com o Azure Active Directory (Azure AD).

Integrar o Google Apps com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooGoogle aplicações
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooGoogle aplicações (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais informações sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do Azure AD com o Google Apps, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Google Apps-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês aqui: [oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).

## <a name="video-tutorial"></a>Tutorial de vídeo
Como tooEnable Single Sign-On tooGoogle aplicações em 2 minutos:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a>Perguntas Mais Frequentes
1. **P: são Chromebooks e outros dispositivos Chrome compatíveis com o Azure AD-início de sessão único?**
   
    R: Sim, os utilizadores são capaz toosign para os respetivos dispositivos Chromebook utilizando as credenciais do Azure AD. Consulte este [Google Apps suporta artigo](https://support.google.com/chrome/a/answer/6060880) para obter informações sobre o motivo os utilizadores podem obter pedidos as credenciais duas vezes.

2. **P: Se ativar a início de sessão único, irão os utilizadores ser capaz toouse os respetivos toosign de credenciais do Azure AD para qualquer produto da Google, tais como o Google sala de aula, GMail, Google Drive, YouTube e assim sucessivamente?**
   
    R: Sim, dependendo da [que aplicações da Google](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) escolha tooenable ou desativar para a sua organização.

3. **P: posso ativar início de sessão para apenas um subconjunto de utilizadores Google Apps?**
   
    R: não, ativar o início de sessão único imediatamente requer que todos os utilizadores Google Apps tooauthenticate com as respetivas credenciais do Azure AD. Porque o Google Apps não suporta a ter vários fornecedores de identidade, fornecedor de identidade Olá para o seu ambiente do Google Apps pode ser do Azure AD ou Google - mas não ambos em Olá mesmo tempo.

4. **P: se um utilizador é iniciada no através do Windows, são que automaticamente se autenticar tooGoogle aplicações sem obter um pedido de uma palavra-passe?**
   
    R: Existem duas opções para ativar este cenário. Em primeiro lugar, os utilizadores foi inicie sessão em dispositivos Windows 10 através de [associação do Azure Active Directory](active-directory-azureadjoin-overview.md). Em alternativa, os utilizadores foi inicie sessão em dispositivos Windows que estão associados a um domínio tooan no local do Active Directory que foi ativada para único início de sessão tooAzure AD através de um [serviços de Federação do Active Directory (AD FS)](active-directory-aadconnect-user-signin.md) implementação. Ambas as opções necessitam passos Olá tooperform Olá seguir tutorial tooenable-início de sessão único entre o Azure AD e o Google Apps.

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Google Apps a partir da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-google-apps-from-hello-gallery"></a>Adicionar Google Apps a partir da Galeria de Olá
tooconfigure Olá integração do Google Apps com o Azure AD, é necessário tooadd Google Apps Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Google Apps a partir da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Google Apps**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. No painel de resultados de Olá, selecione **Google Apps**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com o Google Apps, com base num utilizador de teste chamado "Britta Simon."

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Google Apps é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá no Google Apps tem toobe estabelecida.

Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no Google Apps.

tooconfigure e teste do Azure AD-início de sessão único com o Google Apps, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste do Google Apps](#creating-a-google-apps-test-user)**  -toohave um homólogo de Britta Simon no Google Apps, que é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação do Google Apps.

**tooconfigure do Azure AD-início de sessão único com o Google Apps, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Google Apps** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. No Olá **domínio de aplicações do Google e URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://mail.google.com/a/<yourdomain>`

    > [!NOTE] 
    > Este valor não é real. Atualize o valor de Olá com Olá real URL Sign-on. Contacte Olá [equipa de suporte do Google](https://www.google.com/contact/).
 
4. No Olá **certificado de assinatura de SAML** secção, clique em **certificado** e, em seguida, guarde o certificado de Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. No Olá **configuração de aplicações do Google** secção, clique em **configurar o Google Apps** tooopen **configurar início de sessão** janela. Olá cópia **Sign-Out URL, único início de sessão no URL do serviço SAML e alteração URL de palavra-passe** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. Abra um novo separador no seu browser e inicie sessão no Olá [consola de administração de aplicações do Google](http://admin.google.com/) utilizando a sua conta de administrador.

8. Clique em **segurança**. Se não vir ligação Olá, pode estar ocultado em Olá **mais controlos** menu na parte inferior de Olá do ecrã de Olá.
   
    ![Clique em Security.][10]

9. No Olá **segurança** página, clique em **configurar início de sessão único (SSO).**
   
    ![Clique em SSO.][11]

10. Execute Olá seguintes alterações de configuração:
   
    ![Configurar o SSO][12]
   
    a. Selecione **SSO de configuração com o fornecedor de identidade de terceiros**.

    b. No **URL de página de início de sessão** campo no Google Apps, cole o valor Olá **URL Single Sign-On serviço**, que copiou do portal do Azure.

    c. No Olá **URL da página de início de sessão** campo no Google Apps, cole o valor Olá **Sign-Out URL**, que copiou do portal do Azure. 

    d. No Olá **alterar palavra-passe URL** campo no Google Apps, cole o valor Olá **alterar palavra-passe URL**, que copiou do portal do Azure. 

    e. No Google Apps, para Olá **certificado de verificação**, certificado de Olá de carregamento do que transferiu a partir do portal do Azure.

    f. Clique em **guardar alterações**.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
 
### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-google-apps-test-user"></a>Criar um utilizador de teste do Google Apps

o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon no Software de aplicações do Google. Google Apps suporta o aprovisionamento automático, que é por predefinição ativada. Não há nenhuma ação por si nesta secção. Se um utilizador já não existe no Software de aplicações do Google, uma nova é criada quando tenta tooaccess Software de aplicações do Google.

>[!NOTE] 
>Se precisar de um utilizador de toocreate manualmente, contacte Olá [equipa de suporte do Google](https://www.google.com/contact/).

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooGoogle aplicações.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooGoogle aplicações, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Google Apps**.

    ![Configurar o início de sessão único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, tootest Olá, as único início de sessão definições, abra o painel de acesso em [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), em seguida, iniciar sessão na conta de teste de Olá e, em **Google Apps** mosaico no painel de acesso de Olá.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar o aprovisionamento de utilizadores](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png