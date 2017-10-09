---
title: "Tutorial: Integração do Azure Active Directory Atlassian nuvem | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Atlassian nuvem."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: f679e8b3306bf0efb9373d8baa0cfe095b760aaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a>Tutorial: Integração do Azure Active Directory Atlassian nuvem

Neste tutorial, saiba como toointegrate Atlassian na nuvem com o Azure Active Directory (Azure AD).

Integrar Atlassian Cloud com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooAtlassian na nuvem
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooAtlassian Cloud (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com Atlassian nuvem tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Uma nuvem Atlassian-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês aqui: [oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. A adição de nuvem Atlassian de galeria Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-atlassian-cloud-from-hello-gallery"></a>A adição de nuvem Atlassian de galeria Olá
tooconfigure Olá integração Atlassian nuvem com o Azure AD, é necessário tooadd Atlassian nuvem Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Atlassian da nuvem da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Atlassian nuvem**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. No painel de resultados de Olá, selecione **Atlassian nuvem**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com Atlassian nuvem com base num utilizador de teste chamado "Britta Simon."

Para único início de sessão toowork, do Azure AD tem tooknow qual o utilizador que homólogo Olá na nuvem Atlassian é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá na nuvem Atlassian tem toobe estabelecida.

Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** na nuvem Atlassian.

tooconfigure e teste do Azure AD-início de sessão único com Atlassian nuvem, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste de nuvem Atlassian](#creating-an-atlassian-cloud-test-user)**  -toohave um homólogo de Britta Simon na nuvem Atlassian que é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação de nuvem Atlassian.

**tooconfigure do Azure AD-início de sessão único com Atlassian nuvem, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Atlassian nuvem** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. No Olá **Atlassian nuvem domínio e os URLs** secção, execute os passos seguintes se quiser aplicação Olá tooconfigure de Olá **IDP** iniciada modo:

    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    a. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<instancename>.atlassian.net/admin/saml/edit`

    b. No Olá **URL de resposta** caixa de texto, escreva um URL como:`https://id.atlassian.com/login/saml/acs`

4. Verifique **Mostrar avançadas definições de URL** e efetuar Olá seguir passo se desejar aplicação Olá tooconfigure **SP** iniciada modo:

    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<instancename>.atlassian.net`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualizar estes valores com Olá real identificador e o URL de início de sessão. Pode obter valores exato Olá a partir do ecrã de configuração de SAML do Atlassian na nuvem.
 
5. No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. No Olá **configuração da nuvem Atlassian** secção, clique em **configurar a nuvem de Atlassian** tooopen **configurar início de sessão** janela. Olá cópia **ID de entidade de SAML e único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. tooget SSO configurado para a sua aplicação, o início de sessão toohello Portal Atlassian com direitos de administrador Olá.

8. Na secção autenticação Olá Olá deixado navegação clique **domínios**.

    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    a. Na caixa de texto Olá, escreva o seu nome de domínio e, em seguida, clique em **Adicionar domínio**.
        
    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    b. domínio de Olá tooverify, clique em **verifique**. 

    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    c. Transferir o ficheiro de html de verificação de domínio Olá, carregá-la toohello a pasta raiz do Web site do seu domínio e, em seguida, clique em **verificar domínio**.
    
    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    d. Depois de verificar o domínio de Olá, Olá valor Olá **estado** campo é **Verified**.

    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. Na barra de navegação esquerdo Olá, clique em **SAML**.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. Criar uma configuração de SAML e adicionar a configuração do fornecedor de identidade de Olá.

    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    a. No Olá **fornecedor de identidade ID de entidade** caixa de texto, colar Olá valor **ID de entidade de SAML** que copiou do portal do Azure.

    b. No Olá **fornecedor de identidade SSO URL** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML** que copiou do portal do Azure.

    c. Abra o certificado de Olá transferido do Azure portal cópia Olá valores e sem Olá Begin e linhas de fim e colá-lo na Olá **X509 pública certificado** caixa.
    
    d. Clique em **Guardar configuração** definições de Olá tooSave.
     
11. Atualize Olá do Azure AD definições toomake se de que tem de corrigir o URL de identificador de Olá de configuração.
  
    a. Olá cópia **SP identidade ID** de Olá SAML ecrã e cole-o no Azure AD como Olá **identificador** valor.

    b. URL de início de sessão é Olá URL de inquilino da sua nuvem Atlassian.     

     ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. No portal do Azure Olá, clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-an-atlassian-cloud-test-user"></a>Criar um utilizador de teste Atlassian nuvem

tooenable do Azure AD os utilizadores toolog no tooAtlassian na nuvem, estes têm de ser aprovisionados para Atlassian nuvem.  
Em caso de Atlassian nuvem, o aprovisionamento é uma tarefa manual.

**tooprovision uma conta de utilizador, execute Olá os seguintes passos:**

1. Na secção de administração de sites Olá, clique em Olá **utilizadores** botão

    ![Criar utilizador de nuvem Atlassian](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. Clique em Olá **criar utilizador** botão toocreate um utilizador no Olá Atlassian nuvem

    ![Criar utilizador de nuvem Atlassian](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. Introduza o utilizador Olá **endereço de correio eletrónico**, **Username**, e **nome completo** e atribuir acesso de aplicação Olá. 

    ![Criar utilizador de nuvem Atlassian](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. Clique em **criar utilizador** botão, irá enviar utilizador de toohello de convite de correio eletrónico Olá e após a aceitação de utilizador do Olá convite Olá estará ativo no sistema de Olá. 

>[!NOTE] 
>Também pode criar Olá utilizadores em volume ao clicar em Olá **em massa criar** botão no Olá seção de utilizadores.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooAtlassian na nuvem.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooAtlassian nuvem, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Atlassian nuvem**.

    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração de SSO do Azure AD utilizando Olá painel de acesso.

Ao clicar Olá Atlassian Cloud na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour aplicação Atlassian nuvem. Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

