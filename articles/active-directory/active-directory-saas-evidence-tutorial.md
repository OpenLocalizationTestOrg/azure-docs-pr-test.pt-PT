---
title: "Tutorial: Integração do Azure Active Directory com Evidence.com | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Evidence.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: eed98c15dca8a6a77f0b5d407bb40ee0037fccad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a>Tutorial: Integração do Azure Active Directory com Evidence.com

Neste tutorial, saiba como toointegrate Evidence.com com o Azure Active Directory (Azure AD).

Integrar Evidence.com com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooEvidence.com.
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooEvidence.com (Single Sign-On) com as respetivas contas do Azure AD.
- Pode gerir as contas numa localização central - Olá portal do Azure.

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com Evidence.com tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Evidence.com-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Evidence.com da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-evidencecom-from-hello-gallery"></a>Adicionar Evidence.com da Galeria de Olá
tooconfigure Olá integração de Evidence.com com o Azure AD, é necessário tooadd Evidence.com Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Evidence.com da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![botão de Azure Active Directory Olá][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Painel de aplicações do Olá Enterprise][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![botão de aplicação nova Olá][3]

4. Na caixa de pesquisa de Olá, escreva **Evidence.com**, selecione **Evidence.com** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Evidence.com na lista de resultados de Olá](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD-início de sessão único

Nesta secção, configure e teste do Azure AD-início de sessão único com Evidence.com com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Evidence.com é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Evidence.com tem toobe estabelecida.

No Evidence.com, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com Evidence.com, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Evidence.com](#create-a-evidencecom-test-user)**  -toohave um homólogo de Britta Simon no Evidence.com é toohello ligado do Azure AD de representação do utilizador.
4. **[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Evidence.com.

**tooconfigure do Azure AD-início de sessão único com Evidence.com, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Evidence.com** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar a ligação de início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Caixa de diálogo de início de sessão único](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_samlbase.png)

3. No Olá **Evidence.com domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Domínio Evidence.com e os URLs únicos de informações de início de sessão](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_url.png)

    a. No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<yourtenant>.evidence.com`

    b. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<yourtenant>.evidence.com`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualizar estes valores com Olá real URL de início de sessão e o identificador. Contacte [equipa de suporte de cliente Evidence.com](https://communities.taser.com/support/SupportContactUs?typ=LE) tooget estes valores. 

4. No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![ligação de transferência do certificado Olá](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar botão único início de sessão guardar](./media/active-directory-saas-evidence-tutorial/tutorial_general_400.png)

6. No Olá **Evidence.com configuração** secção, clique em **configurar Evidence.com** tooopen **configurar início de sessão** janela. Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configuração de Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_configure.png) 

7. Numa janela do browser web separado, o início de sessão tooyour Evidence.com como um administrador de inquilino e navegue demasiado**Admin** separador

8. Clique em **Agência início de sessão único**

9. Selecione **SAML baseia início de sessão único**

10. Olá cópia **ID de entidade de SAML**, **único início de sessão no URL do serviço SAML** e **Sign-Out URL** valores apresentados nas Olá portal do Azure e toohello campos correspondente no Evidence.com.

11. Abra o ficheiro transferido do Certificate(Base64) no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência e, em seguida, cole-toohello **certificado de segurança** caixa. 

12. Guarde a configuração de Olá no Evidence.com.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD

o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

   ![Criar um utilizador de teste do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no painel esquerdo Olá, clique em Olá **do Azure Active Directory** botão.

    ![botão de Azure Active Directory Olá](./media/active-directory-saas-evidence-tutorial/create_aaduser_01.png)

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos**e, em seguida, clique em **todos os utilizadores**.

    ![Olá "Utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-evidence-tutorial/create_aaduser_02.png)

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** , Olá parte superior do Olá **todos os utilizadores** caixa de diálogo.

    ![botão de adição de Olá](./media/active-directory-saas-evidence-tutorial/create_aaduser_03.png)

4. No Olá **utilizador** diálogo caixa, execute Olá os seguintes passos:

    ![caixa de diálogo utilizador Olá](./media/active-directory-saas-evidence-tutorial/create_aaduser_04.png)

    a. No Olá **nome** caixa, escreva **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa, tipo Olá endereço de correio eletrónico do utilizador Britta Simon.

    c. Selecione Olá **mostrar palavra-passe** caixa de verificação e, em seguida, anote o valor de Olá que é apresentado no Olá **palavra-passe** caixa.

    d. Clique em **Criar**.
 
### <a name="create-a-evidencecom-test-user"></a>Criar um utilizador de teste Evidence.com

Para o Azure AD os utilizadores toobe capaz de toosign no, têm de ser aprovisionados para acesso no interior Olá Evidence.com aplicação. Esta secção descreve como contas de utilizador toocreate do Azure AD dentro Evidence.com

**uma conta de utilizador no Evidence.com tooprovision:**

1. Numa janela do browser web, inicie sessão no site da sua empresa Evidence.com como administrador.

2. Navegue demasiado**Admin** separador.

3. Clique em **adicionar utilizador**.

4. Clique em Olá **adicionar** botão.

5. Olá **endereço de correio eletrónico** de Olá adicionar utilizador tem de corresponder ao nome de utilizador Olá de utilizadores de Olá no Azure AD que pretende toogive acesso. Se Olá nome de utilizador e endereço de e-mail não são hello mesmo valor na sua organização, pode utilizar Olá **Evidence.com > atributos > Single Sign-On** secção Olá toochange portal do Azure Olá nameidenitifer enviado endereço de e-mail do tooEvidence.com toobe Olá.

### <a name="assign-hello-azure-ad-test-user"></a>Atribua o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooEvidence.com.

![Atribuir a função de utilizador Olá][200] 

**tooassign Britta Simon tooEvidence.com, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Evidence.com**.

    ![ligação de Evidence.com Olá na lista de aplicações de Olá](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_app.png)  

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![ligação de "Utilizadores e grupos" Olá][202]

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição de adicionar Olá][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar em mosaico de Evidence.com Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Evidence.com aplicação.
Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_203.png

