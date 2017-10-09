---
title: "Tutorial: Integração do Azure Active Directory com TargetProcess | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e TargetProcess."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 05c574e2c18d7f73edc6c094093a6e59d46b8e6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a>Tutorial: Integração do Azure Active Directory com TargetProcess

Neste tutorial, saiba como toointegrate TargetProcess com o Azure Active Directory (Azure AD).

Integrar TargetProcess com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooTargetProcess
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooTargetProcess (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com TargetProcess tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um TargetProcess-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar TargetProcess da Galeria de Olá
2. Configurar e testar o Azure AD-início de sessão único

## <a name="add-targetprocess-from-hello-gallery"></a>Adicionar TargetProcess da Galeria de Olá
tooconfigure Olá integração de TargetProcess com o Azure AD, é necessário tooadd TargetProcess Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd TargetProcess da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **TargetProcess**, selecione **TargetProcess** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Adicionar TargetProcess da Galeria](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD-início de sessão único
Nesta secção, configure e teste do Azure AD-início de sessão único com TargetProcess com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá TargetProcess é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá TargetProcess tem toobe estabelecida.

No TargetProcess, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com TargetProcess, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste TargetProcess](#create-a-targetprocess-test-user)**  -toohave um homólogo de Britta Simon no TargetProcess é toohello ligado do Azure AD de representação do utilizador.
4. **[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação TargetProcess.

**tooconfigure do Azure AD-início de sessão único com TargetProcess, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **TargetProcess** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Baseados em SAML início de sessão](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_samlbase.png)

3. No Olá **TargetProcess domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Secção TargetProcess domínio e os URLs](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_url.png)

    a. No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.tpondemand.com/`

    b. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.tpondemand.com/`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualizar estes valores com Olá real URL de início de sessão e o identificador. Contacte [equipa de suporte de cliente TargetProcess](mailto:support@targetprocess.com) tooget estes valores. 
 
4. No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![Secção de certificado de assinatura de SAML](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_certificate.png) 

5. Clique em **guardar** botão.

    ![botão Guardar](./media/active-directory-saas-target-process-tutorial/tutorial_general_400.png)

6. No Olá **TargetProcess configuração** secção, clique em **configurar TargetProcess** tooopen **configurar início de sessão** janela. Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Secção de configuração de TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_configure.png) 

7. Início de sessão tooyour TargetProcess aplicação como um administrador.

8. No menu de Olá na parte superior do Olá, clique em **configuração**.
   
    ![Configurar](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_05.png)

9. Clique em **definições**.
   
    ![Definições](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_06.png) 

10. Clique em **de sessão único-**.
   
    ![Clique em Single Sign-On](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_07.png) 

11. No Olá o início de sessão única caixa de diálogo Definições, execute Olá os seguintes passos:
   
    ![Configurar o início de sessão único](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_08.png)
    
    a. Clique em **ativar o início de sessão único**.
    
    b. No **URL de início de sessão** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML** que copiou do portal do Azure.

    c. Abra o seu certificado transferido no bloco de notas, Olá copiar conteúdo e, em seguida, cole-o Olá **certificado** caixa de texto.
    
    d. Clique em **ativar o aprovisionamento de JIT**.

    e. Clique em **Guardar**.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-target-process-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![lista de Olá toodisplay de utilizadores](./media/active-directory-saas-target-process-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Botão Adicionar](./media/active-directory-saas-target-process-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Secção de utilizador](./media/active-directory-saas-target-process-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="create-a-targetprocess-test-user"></a>Criar um utilizador de teste TargetProcess

o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon TargetProcess.

TargetProcess suportam o aprovisionamento de just-in-time. Que já ativou-lo na [configurar do Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).

Não há nenhum item de ação para si nesta secção.

### <a name="assign-hello-azure-ad-test-user"></a>Atribua o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooTargetProcess.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooTargetProcess, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **TargetProcess**.

    ![TargetProcess na lista de aplicações](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Teste o início de sessão único

o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.

Ao clicar Olá TargetProcess na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour TargetProcess aplicação. Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_203.png

