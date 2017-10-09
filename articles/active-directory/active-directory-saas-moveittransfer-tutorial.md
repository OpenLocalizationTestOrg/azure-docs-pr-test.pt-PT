---
title: "Tutorial: Integração do Azure Active Directory com MOVEit transferência - a integração do Azure AD | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e transferência MOVEit - a integração do Azure AD."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 5bbe4f2d952bd45c4d58d55ffc3467b4eb871fd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a>Tutorial: Integração do Azure Active Directory com MOVEit transferência - a integração do Azure AD

Neste tutorial, saiba como toointegrate MOVEit transferência - integração do Azure AD com o Azure Active Directory (Azure AD).

Integrar MOVEit transferência - integração do Azure AD com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooMOVEit transferência - a integração do Azure AD.
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooMOVEit transferência - integração do Azure AD (Single Sign-On) com as respetivas contas do Azure AD.
- Pode gerir as contas numa localização central - Olá portal do Azure.

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do Azure AD com MOVEit transferência - integração do AD do Azure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Transferência de MOVEit - do Azure AD integração início de sessão único subscrição ativado

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Transferência de MOVEit - integração do Azure AD da Galeria de Olá a adicionar
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-moveit-transfer---azure-ad-integration-from-hello-gallery"></a>Transferência de MOVEit - integração do Azure AD da Galeria de Olá a adicionar
integração de Olá tooconfigure de transferência de MOVEit - integração do Azure AD com o Azure AD, é necessário tooadd MOVEit transferência - integração do Azure AD Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd MOVEit transferência - integração do Azure AD da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![botão de Azure Active Directory Olá][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Painel de aplicações do Olá Enterprise][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![botão de aplicação nova Olá][3]

4. Na caixa de pesquisa de Olá, escreva **MOVEit transferência - a integração do Azure AD**, selecione **MOVEit transferência - a integração do Azure AD** partir do painel de resultados, em seguida, clique em **adicionar** Olá tooadd de botão aplicação.

    ![Transferência de MOVEit - integração do Azure AD na lista de resultados de Olá](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD-início de sessão único

Nesta secção, configure e teste do Azure AD-início de sessão único com MOVEit transferência - integração do Azure AD com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem do utilizador de homólogo Olá na transferência MOVEit tooknow - a integração do Azure AD é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá na transferência MOVEit - a integração do Azure AD tem toobe estabelecida.

Na transferência MOVEit - integração do AD do Azure, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com MOVEit transferência - integração do AD do Azure, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar uma transferência MOVEit - utilizador de teste de integração do Azure AD](#create-a-moveit-transfer---azure-ad-integration-test-user)**  - toohave um homólogo de Britta Simon na transferência MOVEit - integração com o AD do Azure que é toohello ligado do Azure AD de representação do utilizador.
4. **[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua transferência MOVEit - a aplicação de integração do Azure AD.

**tooconfigure do Azure AD-início de sessão único com MOVEit transferência - integração do Azure AD, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **MOVEit transferência - a integração do Azure AD** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar a ligação de início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Caixa de diálogo de início de sessão único](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. No Olá **MOVEit transferência - URLs e integração com o Azure AD domínio** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    a. No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://contoso.com`

    b. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://contoso.com/<tenatid>`

    c. No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`    
     
    > [!NOTE] 
    > Estes valores não estiverem reais. Atualizar estes valores com Olá real identificador, o URL de resposta e o URL de início de sessão. Pode consultar estes valores mais tarde em **URL de metadados do fornecedor de serviço** secção ou contacte [MOVEit transferência - a equipa de suporte de cliente de integração do Azure AD](https://community.ipswitch.com/s/support) tooget estes valores.

4. No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.

    ![ligação de transferência do certificado Olá](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar botão único início de sessão guardar](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. Início de sessão tooyour MOVEit transferência inquilino como administrador.

7. No painel de navegação esquerdo Olá, clique em **definições**.

    ![Lado de secção na aplicação de definições](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. Clique em **Signon único** ligação, que está sob **políticas de segurança -> utilizador Auth**.

    ![Lado de políticas em aplicações de segurança](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. Clique em documento de metadados de Olá ligação toodownload Olá URL de metadados.

    ![URL de metadados do fornecedor de serviço](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * Certifique-se **entityID** corresponde **identificador** no Olá **MOVEit transferência - URLs e integração com o Azure AD domínio** secção.
    * Certifique-se **AssertionConsumerService** corresponde ao URL de localização **URL de resposta** no Olá **MOVEit transferência - URLs e integração com o Azure AD domínio** secção.
    
    ![Configurar lado único início de sessão na aplicação](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. Clique em **Adicionar fornecedor de identidade** botão tooadd um novo fornecedor de identidade federada.

    ![Adicione o fornecedor de identidade](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. Clique em **procurar...**  tooselect Olá o ficheiro de metadados do que transferiu a partir do portal do Azure, em seguida, clique em **Adicionar fornecedor de identidade** Olá tooupload transferido o ficheiro.

    ![Fornecedor de identidade](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. Selecione "**Sim**" como **ativado** no Olá **editar definições do fornecedor de identidade federada...**  página e clique em **guardar**.

    ![Definições do fornecedor de identidade federada](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. No Olá **editar federado identidade do utilizador as definições do fornecedor** página, execute Olá seguintes ações:
    
    ![Editar as definições do fornecedor de identidade federada](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    a. Selecione **SAML NameID** como **nome de início de sessão**.
    
    b. Selecione **outros** como **nome completo** e no Olá **nome de atributo** textbox colocar o valor de Olá: `http://schemas.microsoft.com/identity/claims/displayname`.
    
    c. Selecione **outros** como **E-Mail** e no Olá **nome de atributo** textbox colocar o valor de Olá: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
    
    d. Selecione **Sim** como **Auto-criar conta no signon**.
    
    e. Clique em **guardar** botão.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD

o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

   ![Criar um utilizador de teste do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no painel esquerdo Olá, clique em Olá **do Azure Active Directory** botão.

    ![botão de Azure Active Directory Olá](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos**e, em seguida, clique em **todos os utilizadores**.

    ![Olá "Utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** , Olá parte superior do Olá **todos os utilizadores** caixa de diálogo.

    ![botão de adição de Olá](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. No Olá **utilizador** diálogo caixa, execute Olá os seguintes passos:

    ![caixa de diálogo utilizador Olá](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    a. No Olá **nome** caixa, escreva **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa, tipo Olá endereço de correio eletrónico do utilizador Britta Simon.

    c. Selecione Olá **mostrar palavra-passe** caixa de verificação e, em seguida, anote o valor de Olá que é apresentado no Olá **palavra-passe** caixa.

    d. Clique em **Criar**.
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a>Criar uma transferência MOVEit - utilizador de teste de integração do Azure AD

o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon na transferência MOVEit - a integração do Azure AD. Transferência de MOVEit - integração do AD do Azure suporta just-in-time o aprovisionamento, que tiver ativado. Não há nenhum item de ação para si nesta secção. Um novo utilizador é criado durante uma tentativa tooaccess MOVEit transferência - se de que não existe ainda a integração do AD do Azure.

>[!NOTE]
>Se precisar de um utilizador de toocreate manualmente, terá de toocontact Olá [MOVEit transferência - a equipa de suporte de cliente de integração do Azure AD](https://community.ipswitch.com/s/support).

### <a name="assign-hello-azure-ad-test-user"></a>Atribua o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooMOVEit transferência - a integração do Azure AD.

![Atribuir a função de utilizador Olá][200] 

**tooassign Britta Simon tooMOVEit transferência - integração do Azure AD, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **MOVEit transferência - a integração do Azure AD**.

    ![ligação de integração do Azure AD Hello MOVEit transferência - na lista de aplicações de Olá](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![ligação de "Utilizadores e grupos" Olá][202]

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição de adicionar Olá][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Teste o início de sessão único

o objetivo desta secção Olá é tootest a configuração de SSO do Azure AD utilizando Olá painel de acesso.

Ao clicar em Olá MOVEit transferência - mosaico de integração do Azure AD no painel de acesso Olá, deve obter automaticamente com sessão iniciada tooyour MOVEit transferência - a aplicação de integração do Azure AD. 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

