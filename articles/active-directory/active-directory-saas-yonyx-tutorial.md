---
title: "Tutorial: Integração do Azure Active Directory com guias interativa Yonyx | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e guias interativa Yonyx."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 07db4e01-319b-4cb6-9b93-4577bffd3cbc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: 24e30d243143651b8d32535c76dc300931ae5746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-yonyx-interactive-guides"></a>Tutorial: Integração do Azure Active Directory com guias interativa Yonyx

Neste tutorial, saiba como toointegrate Yonyx interativo guias no Azure Active Directory (Azure AD).

Guias de interativa Yonyx a integração com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooYonyx guias interativa
- Pode ativar a utilizadores tooautomatically get com sessão iniciada tooYonyx guias interativa (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com guias interativa Yonyx tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um guias interativa Yonyx-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. A adição de guias interativa Yonyx de galeria Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-yonyx-interactive-guides-from-hello-gallery"></a>A adição de guias interativa Yonyx de galeria Olá
tooconfigure Olá integração guias interativa Yonyx com o Azure AD, é necessário tooadd Yonyx guias interativa Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Yonyx guias interativo na Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![botão de Azure Active Directory Olá][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Painel de aplicações do Olá Enterprise][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![botão de aplicação nova Olá][3]

4. Na caixa de pesquisa de Olá, escreva **guias interativa Yonyx**, selecione **guias interativa Yonyx** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Guias de interativa Yonyx na lista de resultados de Olá](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD-início de sessão único

Nesta secção, configure e teste do Azure AD-início de sessão único com os guias de interativa Yonyx com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow qual o utilizador que homólogo Olá guias interativa Yonyx é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e relacionados com o utilizador Olá guias interativa Yonyx tem toobe estabelecida.

Guias de interativa Yonyx, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com guias interativa Yonyx, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste de guias interativa Yonyx](#create-a-yonyx-interactive-guides-test-user)**  -toohave um homólogo de Britta Simon Yonyx guias interativas que é toohello ligado do Azure AD de representação do utilizador.
4. **[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação guias interativa Yonyx.

**tooconfigure do Azure AD-início de sessão único com guias de interativa Yonyx, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **guias interativa Yonyx** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar a ligação de início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Caixa de diálogo de início de sessão único](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_samlbase.png)

3. No Olá **Yonyx interativa guias de domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Yonyx interativa guias de domínio e os URLs únicos de informações de início de sessão](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_url.png)

    a. No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company name>.yonyx.com/y/conversation/?id=<guid number>`

    b. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company name>.yonyx.com`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualizar estes valores com Olá real URL de início de sessão e o identificador. Contacte [equipa de suporte de cliente de guias interativa Yonyx](mailto:support@yonyx.com) tooget estes valores. 
 
4. No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![ligação de transferência do certificado Olá](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar botão único início de sessão guardar](./media/active-directory-saas-yonyx-tutorial/tutorial_general_400.png)

6. No Olá **Yonyx interativa guias de configuração** secção, clique em **configurar interativa guias de Yonyx** tooopen **configurar início de sessão** janela. Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configuração de guias interativa Yonyx](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_configure.png) 

7. tooconfigure-início de sessão único em **guias interativa Yonyx** lado, terá de Olá toosend transferido **Certificate(Base64)**, **Sign-Out URL**, **SAML Single Sign-On URL do serviço** **ID de entidade de SAML** demasiado[guias interativa Yonyx suporta equipa](mailto:support@yonyx.com). Configuram Olá de toohave esta definição corretamente em ambos os lados de ligação de SAML SSO.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="create-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD

o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

  ![Criar um utilizador de teste do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![botão de Azure Active Directory Olá](./media/active-directory-saas-yonyx-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Olá "Utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-yonyx-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![botão de adição de Olá](./media/active-directory-saas-yonyx-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![caixa de diálogo utilizador Olá](./media/active-directory-saas-yonyx-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="create-a-yonyx-interactive-guides-test-user"></a>Criar um utilizador de teste de guias interativa Yonyx

o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon guias interativa Yonyx. Guias de interativa Yonyx suportam o aprovisionamento de just-in-time, que é por predefinição ativada.

Não há nenhum item de ação para si nesta secção. Um novo utilizador é criado durante uma tentativa tooaccess guias interativa Yonyx se não existir ainda.

>[!NOTE]
>Se precisar de um utilizador de toocreate manualmente, terá de Olá toocontact guias interativa Yonyx suporta equipa através de < mailto:support@yonyx.com >. 

### <a name="assign-hello-azure-ad-test-user"></a>Atribua o utilizador de teste de Olá do Azure AD

Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooYonyx guias interativo.

![Atribuir a função de utilizador Olá][200]

**tooassign Britta Simon tooYonyx interativa manuais, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **guias interativa Yonyx**.

    ![Olá guias interativa Yonyx ligação na lista de aplicações de Olá](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![ligação de "Utilizadores e grupos" Olá][202]

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição de adicionar Olá][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar Olá guias interativa Yonyx na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour aplicação guias interativa Yonyx.

Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_203.png

