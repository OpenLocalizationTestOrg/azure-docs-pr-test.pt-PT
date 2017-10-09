---
title: "Tutorial: Integração do Azure Active Directory com PurelyHR | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e PurelyHR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 86a9c454-596d-4902-829a-fe126708f739
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: bdc1748ed650cff36b1ef7d7330dd2a17b3bc760
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-purelyhr"></a>Tutorial: Integração do Azure Active Directory com PurelyHR

Neste tutorial, saiba como toointegrate PurelyHR com o Azure Active Directory (Azure AD).

Integrar PurelyHR com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooPurelyHR
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooPurelyHR (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com PurelyHR tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um PurelyHR início de sessão único subscrição ativado

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar PurelyHR da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-purelyhr-from-hello-gallery"></a>Adicionar PurelyHR da Galeria de Olá
tooconfigure Olá integração de PurelyHR com o Azure AD, é necessário tooadd PurelyHR Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd PurelyHR da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **PurelyHR**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_search.png)

5. No painel de resultados de Olá, selecione **PurelyHR**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com PurelyHR com base num utilizador de teste chamado "Britta Simon."

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá PurelyHR é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá PurelyHR tem toobe estabelecida.

No PurelyHR, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com PurelyHR, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste PurelyHR](#creating-a-purelyhr-test-user)**  -toohave um homólogo de Britta Simon no PurelyHR é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação PurelyHR.

**tooconfigure do Azure AD-início de sessão único com PurelyHR, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **PurelyHR** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_samlbase.png)

3. No Olá **PurelyHR domínio e os URLs** secção, execute os passos seguintes se quiser aplicação Olá tooconfigure de Olá **IDP** iniciada modo:

    ![Configurar o início de sessão único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url.png)
   
    No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyID>.purelyhr.com/sso-consume`

4. Verifique **Mostrar avançadas definições de URL**, se desejar aplicação Olá tooconfigure **SP** iniciada modo:

    ![Configurar o início de sessão único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url1.png)
    
    No Olá **URL de início de sessão** caixa de texto, o valor do tipo Olá Olá seguir o padrão de utilização:`https://<companyID>.purelyhr.com/sso-initiate`
     
    > [!NOTE]
    > Estes valores não estiverem Olá real. Atualize estes valores com o URL de resposta real Olá e o URL de início de sessão. Contacte [equipa de suporte de cliente PurelyHR](http://support.purelyhr.com/) tooget estes valores. 

5. No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_certificate.png) 

6. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-purelyhr-tutorial/tutorial_general_400.png)
    
7. No Olá **PurelyHR configuração** secção, clique em **configurar PurelyHR** tooopen **configurar início de sessão** janela. Olá cópia **ID de entidade de SAML e único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_configure.png) 

8. tooconfigure-início de sessão único em **PurelyHR** lado, o Web site tootheir de início de sessão como administrador.

9. Abra Olá **Dashboard** das opções de Olá na barra de ferramentas Olá e clique em **SSO definições**.

10. Colar Olá valores nas caixas de Olá como descrito abaixo-

    ![Configurar o início de sessão único](./media/active-directory-saas-purelyhr-tutorial/purelyhr-dashboard-sso-settings.png)    

    a. Abra Olá **Certificate(Bas64)** transferido a partir de Olá portal do Azure no bloco de notas e copie-valor do certificado Olá. Olá colar copiados valor para Olá **certificado x. 509** caixa.

    b. No Olá **URL do emissor Idp** caixa, cole Olá **ID de entidade de SAML** copiados Olá portal do Azure.

    c. No Olá **URL de ponto final do Idp** caixa, cole Olá **único início de sessão no URL do serviço SAML** copiados Olá portal do Azure. 

    d. Verifique Olá **Auto-criar utilizadores** caixa de verificação o aprovisionamento de utilizador automáticas de tooenable no PurelyHR.

    e. Clique em **guardar alterações** definições de Olá toosave.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-purelyhr-test-user"></a>Criar um utilizador de teste PurelyHR

tooenable do Azure AD os utilizadores toolog no tooPurelyHR, estes têm de ser aprovisionados para PurelyHR. PurelyHR, o aprovisionamento é uma tarefa automática e não existem passos manuais são necessários quando o aprovisionamento de utilizadores automático está ativado.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooPurelyHR.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooPurelyHR, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **PurelyHR**.

    ![Configurar o início de sessão único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Clique em Olá absorver LMS na peça de mosaico Olá painel de acesso, obter aplicações de absorver LMS tooyour automaticamente com sessão iniciada.

Para obter mais informações sobre Olá painel de acesso, consulte. [No painel de acesso do introdução toohello](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_203.png

