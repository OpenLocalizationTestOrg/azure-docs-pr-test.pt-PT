---
title: "Tutorial: Integração do Azure Active Directory com SkyDesk E-Mail | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e SkyDesk E-Mail."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9d0bbcb-ddb5-473f-a4aa-028ae88ced1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 19c670a60f581a2be55b74eacdb5393a36e38be3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skydesk-email"></a>Tutorial: Integração do Azure Active Directory com SkyDesk E-Mail

Neste tutorial, saiba como toointegrate SkyDesk E-Mail com o Azure Active Directory (Azure AD).

Integrar SkyDesk E-Mail com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooSkyDesk E-Mail
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooSkyDesk E-Mail (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com o E-Mail SkyDesk tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um E-Mail SkyDesk-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês aqui [oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar SkyDesk E-Mail a partir da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-skydesk-email-from-hello-gallery"></a>Adicionar SkyDesk E-Mail a partir da Galeria de Olá
tooconfigure Olá integração de SkyDesk E-Mail com o Azure AD, é necessário tooadd SkyDesk E-Mail Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd SkyDesk E-Mail na Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **SkyDesk E-Mail**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_search.png)

5. No painel de resultados de Olá, selecione **SkyDesk E-Mail**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configura e teste do Azure AD-início de sessão único com SkyDesk E-Mail com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow qual o utilizador que homólogo Olá no E-Mail de SkyDesk é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o Olá utilizador relacionados na mensagem de correio eletrónico SkyDesk tem toobe estabelecida.

No E-Mail de SkyDesk, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com SkyDesk E-Mail, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste de E-Mail SkyDesk](#creating-a-skydesk-email-test-user)**  -toohave um homólogo de Britta Simon SkyDesk por correio eletrónico que é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação de E-Mail SkyDesk.

**tooconfigure do Azure AD-início de sessão único com SkyDesk E-Mail, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **SkyDesk E-Mail** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_samlbase.png)

3. No Olá **URLs e de domínio de correio eletrónico SkyDesk** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_url.png)

    No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://mail.skydesk.jp/portal/<companyname>`

    > [!NOTE] 
    > o valor de Olá não é real. Atualização Olá valor com Olá real URL de início de sessão. Contacte [equipa de suporte de cliente de E-Mail SkyDesk](https://www.skydesk.sg/support/) valor de Olá tooget. 
 
4. No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_400.png)

6. No Olá **configuração do E-Mail SkyDesk** secção, clique em **configurar E-Mail de SkyDesk** tooopen **configurar início de sessão** janela. Olá cópia **Sign-Out URL e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_configure.png) 

7. tooenable SSO no **SkyDesk E-Mail**, efetuar Olá os seguintes passos:

    a. Início de sessão tooyour conta de E-Mail de SkyDesk como administrador.

    b. No menu de Olá na parte superior do Olá, clique em **configuração**e selecione **Org**. 
    
      ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_51.png)
  
    c. Clique em **domínios** partir do painel esquerdo Olá.
    
      ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_53.png)

    d. Clique em **Adicionar domínio**.
    
      ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_54.png)

    e. Introduza o nome de domínio e, em seguida, certifique-se Olá domínio.
    
      ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_55.png)

    f. Clique em **autenticação SAML** partir do painel esquerdo Olá.
    
      ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_52.png)

8. No Olá **autenticação SAML** diálogo página, execute Olá os seguintes passos:
   
      ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_56.png)
   
    >[!NOTE]
    >autenticação com base no toouse SAML, deve ter **domínio verificado** ou **portal URL** programa de configuração. Pode definir portal Olá URL com nome exclusivo Olá.
    > 
    > 
   
    ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_57.png)

    a. No Olá **URL de início de sessão** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML**, que copiou do portal do Azure.
   
    b. No Olá **terminar** caixa de texto do URL, colar Olá valor **Sign-Out URL**, que copiou do portal do Azure.

    c. **Altere o URL de palavra-passe** é opcional, por isso, pode deixar em branco.

    d. Clique em **obter chave a partir de um ficheiro** tooselect o certificado transferido do portal do Azure e, em seguida, clique em **abra** certificado de Olá tooupload.

    e. Como **algoritmo**, selecione **RSA**.

    f. Clique em **Ok** alterações de Olá toosave.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-skydesk-email-test-user"></a>Criar um utilizador de teste SkyDesk E-Mail

Nesta secção, vai criar um utilizador chamado Britta Simon no E-Mail de SkyDesk.

1. Clique em **acesso de utilizador** Olá deixado painel no E-Mail de SkyDesk e, em seguida, introduza o nome de utilizador. 

    ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_58.png)

>[!NOTE] 
>Se precisar de utilizadores em massa de toocreate, terá de toocontact Olá [equipa de suporte de cliente de E-Mail SkyDesk](https://www.skydesk.sg/support/).


### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooSkyDesk E-Mail.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooSkyDesk E-Mail, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **SkyDesk E-Mail**.

    ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

o objetivo desta secção Olá é tootest a configuração de SSO do Azure AD utilizando Olá painel de acesso.

Ao clicar Olá SkyDesk E-Mail na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour aplicação SkyDesk E-Mail.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_203.png

