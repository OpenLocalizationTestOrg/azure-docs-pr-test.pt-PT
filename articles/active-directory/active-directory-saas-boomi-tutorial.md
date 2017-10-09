---
title: "Tutorial: Integração do Azure Active Directory com Boomi | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Boomi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ce64a4561697d311a8c7b1b244315bb552c5cfb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a>Tutorial: Integração do Azure Active Directory com Boomi

Neste tutorial, saiba como toointegrate Boomi com o Azure Active Directory (Azure AD).

Integrar Boomi com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooBoomi
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooBoomi (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com Boomi tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Boomi-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Boomi da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-boomi-from-hello-gallery"></a>Adicionar Boomi da Galeria de Olá
tooconfigure Olá integração de Boomi com o Azure AD, é necessário tooadd Boomi Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Boomi da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Boomi**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. No painel de resultados de Olá, selecione **Boomi**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com Boomi com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Boomi é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Boomi tem toobe estabelecida.

No Boomi, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com Boomi, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Boomi](#creating-a-boomi-test-user)**  -toohave um homólogo de Britta Simon no Boomi é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Boomi.

**tooconfigure do Azure AD-início de sessão único com Boomi, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **Boomi** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. No Olá **Boomi domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    a. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://platform.boomi.com/sso/<accountname>/saml`

    b. No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://platform.boomi.com/sso/<accountname>/saml`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualize estes valores com o URL de identificador e resposta real no Olá. Contacte [equipa de suporte de Boomi](https://boomi.com/company/contact/) tooget estes valores.

4. No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.
    
    ![Configurar o início de sessão único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. Aplicação de Boomi espera asserções de SAML Olá num formato específico. Configure Olá seguintes afirmações para esta aplicação. Pode gerir os valores de Olá destes atributos a partir de Olá "**atributos de utilizador**" secção na página de integração de aplicações. Olá seguinte captura de ecrã mostra um exemplo para este.
    
    ![Configurar o início de sessão único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. No Olá **atributos de utilizador** secção em Olá **de sessão único-** caixa de diálogo, para cada linha mostrada na tabela de Olá abaixo, efetue Olá os seguintes passos:

    | Nome do atributo | Valor do atributo |
    | -------------- | --------------- |
    | FEDERATION_ID | User.Mail |
    
    a. Clique em **adicionar atributo** tooopen Olá **adicionar atributo** caixa de diálogo.
    
    ![Configurar o início de sessão único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Configurar o início de sessão único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    b. No Olá **nome** caixa de texto, nome de atributo do tipo Olá mostrado para essa linha.
    
    c. De Olá **valor** lista, o valor de atributo do tipo Olá mostrado para essa linha.
    
    d. Clique em **OK**.

6. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. No Olá **Boomi configuração** secção, clique em **configurar Boomi** tooopen **configurar início de sessão** janela. Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. Numa janela do browser web diferente, inicie sessão no site da sua empresa Boomi como administrador. 

9. Navegue demasiado**nome da empresa** e aceda demasiado**configurar**.

10. Clique em Olá **SSO opções** separador e executar passos abaixo.

    ![Configurar o início de sessão único no lado de aplicação](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    a. Verifique **ativar SAML Single Sign-On** caixa de verificação.

    b. Clique em **importação** Olá tooupload transferido certificado a partir do Azure AD demasiado**certificado do fornecedor de identidade**.
    
    c. No Olá **URL de início de sessão do fornecedor de identidade** caixa de texto, coloque o valor Olá **único início de sessão no URL do serviço SAML** da janela de configuração de aplicação do Azure AD.

    d. Como **Federação Id localização**, selecione **Id de Federação é no elemento de atributo FEDERATION_ID** botão de opção. 

    e. Clique em **guardar** botão.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-boomi-test-user"></a>Criar um utilizador de teste Boomi

Na ordem tooenable do Azure AD os utilizadores toolog no tooBoomi, têm de ser aprovisionados para Boomi. No caso de Olá da Boomi, o aprovisionamento é uma tarefa manual.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>tooprovision uma conta de utilizador, execute Olá os seguintes passos:

1. Inicie sessão no tooyour Boomi site da empresa como administrador.

2. Após iniciar sessão, navegue até demasiado**gestão de utilizadores** e aceda demasiado**utilizadores**.

    ![Os utilizadores](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "utilizadores")

3. Clique em  **+**  ícone e Olá **funções de utilizador de adicionar/manter** abre a caixa de diálogo.

    ![Os utilizadores](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "utilizadores")

    ![Os utilizadores](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "utilizadores")

    a. No Olá **endereço de correio eletrónico do utilizador** caixa de texto, como o tipo Olá e-mail do utilizador BrittaSimon@contoso.com.
    
    b. No Olá **nome próprio** caixa de texto, tipo Olá primeiro nome de utilizador como Britta.

    c. No Olá **Apelido** caixa de texto, tipo Olá apelido do utilizador como Simon.
    
    d. Introduza o utilizador Olá **ID de Federação**. Cada utilizador tem de ter um ID de federação que identifica exclusivamente o utilizador de Olá numa conta Olá.
    
    e. Atribuir Olá **utilizador padrão** utilizador toohello de função. Não atribua a função de administrador Olá porque que deverá dar-lhe normal Atmosphere acesso, bem como o acesso de início de sessão único.
    
    f. Clique em **OK**.
    
    > [!NOTE]
    > utilizador Olá não irá receber um e-mail de notificação de boas-vindas com uma palavra-passe que pode ser utilizado toolog no toohello AtomSphere conta porque a palavra-passe é gerida através do fornecedor de identidade Olá. Pode utilizar quaisquer outras Boomi utilizador conta criação ferramentas ou APIs fornecidas pelo Boomi tooprovision contas de utilizador do AAD. 

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooBoomi.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooBoomi, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Boomi**.

    ![Configurar o início de sessão único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar em mosaico de Boomi Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Boomi aplicação.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

