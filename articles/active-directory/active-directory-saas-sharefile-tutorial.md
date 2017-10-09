---
title: "Tutorial: Integração do Azure Active Directory com Citrix ShareFile | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Citrix ShareFile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: d7eaf140e56c40f9f621062849dd8558588ffd1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a>Tutorial: Integração do Azure Active Directory com Citrix ShareFile

Neste tutorial, saiba como toointegrate Citrix ShareFile com o Azure Active Directory (Azure AD).

Integrar o Citrix ShareFile com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooCitrix ShareFile.
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooCitrix ShareFile (Single Sign-On) com as respetivas contas do Azure AD.
- Pode gerir as contas numa localização central - Olá portal do Azure.

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com Citrix ShareFile tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Citrix ShareFile-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Citrix ShareFile da Galeria de Olá
2. Configurar e testar o Azure AD-início de sessão único

## <a name="add-citrix-sharefile-from-hello-gallery"></a>Adicionar Citrix ShareFile da Galeria de Olá
tooconfigure Olá integração da Citrix ShareFile com o Azure AD, é necessário tooadd Citrix ShareFile Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Citrix ShareFile da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![botão de Azure Active Directory Olá][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Painel de aplicações do Olá Enterprise][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![botão de aplicação nova Olá][3]

4. Na caixa de pesquisa de Olá, escreva **Citrix ShareFile**, selecione **Citrix ShareFile** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Lista de resultados da Citrix ShareFile no Olá](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD-início de sessão único

Nesta secção, configure e teste do Azure AD-início de sessão único com Citrix ShareFile baseado na chamado "Britta Simon" um utilizador de teste.

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Citrix ShareFile é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Citrix ShareFile tem toobe estabelecida.

No Citrix ShareFile, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com Citrix ShareFile, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste do Citrix ShareFile](#create-a-citrix-sharefile-test-user)**  -toohave um homólogo de Britta Simon no Citrix ShareFile que é toohello ligado do Azure AD de representação do utilizador.
4. **[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Citrix ShareFile.

**tooconfigure do Azure AD-início de sessão único com Citrix ShareFile, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Citrix ShareFile** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar a ligação de início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Caixa de diálogo de início de sessão único](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. No Olá **Citrix ShareFile domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Citrix ShareFile domínio e os URLs únicos de informações de início de sessão](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenant-name>.sharefile.com/saml/login`

    > [!NOTE] 
    > Este valor não é real. Atualizar este valor com Olá real URL de início de sessão. Contacte [equipa de suporte de cliente do Citrix ShareFile](https://www.citrix.co.in/products/sharefile/support.html) tooget este valor. 

4. No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![ligação de transferência do certificado Olá](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar botão único início de sessão guardar](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. No Olá **configuração da Citrix ShareFile** secção, clique em **configurar ShareFile de Citrix** tooopen **configurar início de sessão** janela. Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configuração da Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. Numa janela do browser web diferente, inicie sessão no seu **Citrix ShareFile** site da empresa como administrador.

8. Na barra de ferramentas Olá na parte superior do Olá, clique em **Admin**.

9. No painel de navegação esquerdo Olá, selecione **configurar Single Sign-On**.
   
    ![Conta de administração](./media/active-directory-saas-sharefile-tutorial/ic773627.png "administração da conta")

10. No Olá **Single Sign-On / SAML 2.0 configuração** página da caixa de diálogo em **definições básicas**, efetuar Olá os seguintes passos:
   
    ![De sessão único-](./media/active-directory-saas-sharefile-tutorial/ic773628.png "de sessão único-")
   
    a. Clique em **ativar SAML**.
    
    b. No **o emissor de IDP / ID de entidade** caixa de texto, colar Olá valor **ID de entidade de SAML** que copiou do portal do Azure.

    c. Clique em **alteração** toohello seguinte **certificado x. 509** Olá, campo e, em seguida, o certificado de Olá de carregamento transferiu a partir do portal do Azure.
    
    d. No **URL de início de sessão** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML** que copiou do portal do Azure.
    
    e. No **URL de fim de sessão** caixa de texto, colar Olá valor **Sign-Out URL** que copiou do portal do Azure.

11. Clique em **guardar** no Olá portal de gestão do Citrix ShareFile.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD

o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

   ![Criar um utilizador de teste do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no painel esquerdo Olá, clique em Olá **do Azure Active Directory** botão.

    ![botão de Azure Active Directory Olá](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos**e, em seguida, clique em **todos os utilizadores**.

    ![Olá "Utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** , Olá parte superior do Olá **todos os utilizadores** caixa de diálogo.

    ![botão de adição de Olá](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. No Olá **utilizador** diálogo caixa, execute Olá os seguintes passos:

    ![caixa de diálogo utilizador Olá](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    a. No Olá **nome** caixa, escreva **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa, tipo Olá endereço de correio eletrónico do utilizador Britta Simon.

    c. Selecione Olá **mostrar palavra-passe** caixa de verificação e, em seguida, anote o valor de Olá que é apresentado no Olá **palavra-passe** caixa.

    d. Clique em **Criar**.
 
### <a name="create-a-citrix-sharefile-test-user"></a>Criar um utilizador de teste Citrix ShareFile

Na ordem tooenable do Azure AD os utilizadores toolog para Citrix ShareFile, têm de ser aprovisionados para Citrix ShareFile. No caso de Olá da Citrix ShareFile, o aprovisionamento é uma tarefa manual.

**tooprovision uma conta de utilizador, execute Olá os seguintes passos:**

1. Inicie sessão no tooyour **Citrix ShareFile** inquilino.

2. Clique em **gerir utilizadores \> gerir utilizadores Home \> + criar empregado**.
   
   ![Criar empregado](./media/active-directory-saas-sharefile-tutorial/IC781050.png "criar empregado")

3. No Olá **informações básicas** secção, execute passos abaixo:
   
   ![Informações básicas](./media/active-directory-saas-sharefile-tutorial/IC799951.png "informações básicas")
   
   a. No Olá **endereço de correio eletrónico** caixa de texto, endereço de correio eletrónico do tipo Olá de Britta Simon como  **brittasimon@contoso.com** .
   
   b. No Olá **nome próprio** caixa de texto, tipo **nome próprio** do utilizador como **Britta**.
   
   c. No Olá **Apelido** caixa de texto, tipo **Apelido** do utilizador como **Simon**.

4. Clique em **adicionar utilizador**.
  
   >[!NOTE]
   >titular da conta do Olá do Azure AD irá receber um e-mail e siga a tooconfirm uma ligação a respetiva conta para ficar ativa. Pode utilizar quaisquer outras Citrix ShareFile utilizador conta criação ferramentas ou APIs fornecidas pelo Citrix ShareFile tooprovision contas de utilizador do Azure AD.

### <a name="assign-hello-azure-ad-test-user"></a>Atribua o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooCitrix ShareFile.

![Atribuir a função de utilizador Olá][200] 

**tooassign Britta Simon tooCitrix ShareFile, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Citrix ShareFile**.

    ![Olá Citrix ShareFile ligação na lista de aplicações de Olá](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![ligação de "Utilizadores e grupos" Olá][202]

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição de adicionar Olá][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar Olá Citrix ShareFile na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour aplicação Citrix ShareFile.
Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

