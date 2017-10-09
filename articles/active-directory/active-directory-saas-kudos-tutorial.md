---
title: "Tutorial: Integração do Azure Active Directory com Kudos | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Kudos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 39c47ce6-4944-47ba-8f53-3afa95398034
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: c1b481463574461f9948db2b83843fefa5d74e99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kudos"></a>Tutorial: Integração do Azure Active Directory com Kudos

Neste tutorial, saiba como toointegrate Kudos com o Azure Active Directory (Azure AD).

Integrar Kudos com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooKudos
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooKudos (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com Kudos tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Kudos-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Kudos da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-kudos-from-hello-gallery"></a>Adicionar Kudos da Galeria de Olá
tooconfigure Olá integração de Kudos com o Azure AD, é necessário tooadd Kudos Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Kudos da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Kudos**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_search.png)

5. No painel de resultados de Olá, selecione **Kudos**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com Kudos com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Kudos é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Kudos tem toobe estabelecida.

No Kudos, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com Kudos, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Kudos](#creating-a-kudos-test-user)**  -toohave um homólogo de Britta Simon no Kudos é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Kudos.

**tooconfigure do Azure AD-início de sessão único com Kudos, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Kudos** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_samlbase.png)

3. No Olá **Kudos domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_url.png)

    No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company>.kudosnow.com`
    
    > [!NOTE] 
    > Este valor não é real. Atualizar este valor com Olá real URL de início de sessão. Contacte [equipa de suporte de cliente Kudos](http://success.kudosnow.com/home) tooget este valor. 
 
4. No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-kudos-tutorial/tutorial_general_400.png)

6. No Olá **Kudos configuração** secção, clique em **configurar Kudos** tooopen **configurar início de sessão** janela. Olá cópia **Sign-Out URL e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_configure.png) 

7. Numa janela do browser web diferente, inicie sessão no site da sua empresa Kudos como administrador.

8. No menu de Olá na parte superior do Olá, clique em **definições**.
   
    ![Definições](./media/active-directory-saas-kudos-tutorial/ic787806.png "definições")

9. Clique em **integrações \> SSO**.

10. No Olá **SSO** secção, execute Olá os seguintes passos:
   
    ![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")
   
    a. No **iniciar sessão no URL** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML** que copiou do portal do Azure. 

    b. Abra o certificado codificado base-64 no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência e, em seguida, cole-toohello **certificado x. 509** caixa de texto
   
    c. No **tooURL de fim de sessão**, cole o valor Olá **Sign-Out URL** que copiou do portal do Azure.
   
    d. No Olá **seu URL de Kudos** caixa de texto, escreva o nome da sua empresa.
   
    e. Clique em **Guardar**.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-kudos-test-user"></a>Criar um utilizador de teste Kudos

Na ordem tooenable do Azure AD os utilizadores toolog para Kudos, têm de ser aprovisionados para Kudos. 

No caso de Olá da Kudos, o aprovisionamento é uma tarefa manual.

**tooprovision uma conta de utilizador, execute Olá os seguintes passos:**

1. Inicie sessão no tooyour **Kudos** site da empresa como administrador.

2. No menu de Olá na parte superior do Olá, clique em **definições**.
   
   ![Definições](./media/active-directory-saas-kudos-tutorial/ic787806.png "definições")

3. Clique em **utilizador Admin**.

4. Clique em Olá **utilizadores** separador e, em seguida, clique em **adicionar um utilizador**.
   
   ![Utilizador Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "utilizador Admin")

5. No Olá **adicionar um utilizador** secção, execute Olá os seguintes passos:
   
    ![Adicionar um utilizador](./media/active-directory-saas-kudos-tutorial/ic787810.png "adicionar um utilizador")
   
    a. Olá tipo **nome próprio**, **Apelido**, **E-Mail** e outros detalhes de uma conta válida do Azure Active Directory que pretende tooprovision Olá relacionadas com caixas de texto.
   
    b. Clique em **criar utilizador**.

>[!NOTE]
>Pode utilizar quaisquer outras Kudos utilizador conta criação ferramentas ou APIs fornecidas pelo Kudos tooprovision contas de utilizador do AAD.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooKudos.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooKudos, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Kudos**.

    ![Configurar o início de sessão único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar em mosaico de Kudos Olá no painel de acesso de Olá, deve obter a aplicação de Kudos tooyour automaticamente com sessão iniciada. Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_203.png

