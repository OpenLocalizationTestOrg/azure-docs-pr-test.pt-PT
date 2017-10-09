---
title: "Tutorial: Integração do Azure Active Directory com o Procore SSO | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Procore SSO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: bb918617f18ba3f44ddde469e6fc411977752f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a>Tutorial: Integração do Azure Active Directory com o Procore SSO

Neste tutorial, saiba como toointegrate Procore SSO ao Azure Active Directory (Azure AD).

Integrar o Procore SSO com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooProcore SSO
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooProcore SSO (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - portal de gestão do Azure de Olá

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Procore SSO, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com o Procore SSO tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um Procore SSO início de sessão único subscrição ativado

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. A adição de Procore SSO de galeria Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-procore-sso-from-hello-gallery"></a>A adição de Procore SSO de galeria Olá
tooconfigure Olá integração do Procore SSO com o Azure AD, é necessário tooadd Procore SSO Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd SSO Procore da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[Azure Management Portal](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. Clique em **adicionar** botão na parte superior de Olá da caixa de diálogo Olá.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **Procore SSO**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. No painel de resultados de Olá, selecione **Procore SSO**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com o SSO Procore com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Procore SSO é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Procore SSO tem toobe estabelecida.

Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** em Procore SSO.

tooconfigure e teste do Azure AD-início de sessão único com o Procore SSO, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste de Procore SSO](#creating-a-procore-sso-test-user)**  -toohave um homólogo de Britta Simon em Procore SSO que é a representação de toohello ligado do Azure AD de forma.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD início de sessão no portal de gestão do Azure Olá e configurar o início de sessão único na sua aplicação Procore SSO.

**tooconfigure do Azure AD-início de sessão único com o Procore SSO, execute Olá os seguintes passos:**

1. No portal de gestão do Azure de Olá, no Olá **Procore SSO** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. No Olá **Procore de SSO de domínio e os URLs** secção, hello utilizador não tem tooperform quaisquer passos conforme Olá aplicação já está pré-integrada com o Azure.

    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro XML de Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. No Olá **Procore SSO configuração** secção, clique em **configurar Procore SSO** tooopen **configurar início de sessão** janela. Olá cópia **ID de entidade de SAML e único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. tooconfigure-início de sessão único em **Procore SSO** lado, o site de empresa procore de tooyour de início de sessão como administrador.

8. Na lista de caixa de ferramentas de Olá pendente, clique em **Admin** página de definições do tooopen Olá SSO.

    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. Colar Olá valores nas caixas de Olá como descrito abaixo-

    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    a. No Olá **único início de sessão no URL do emissor** caixa, cole Olá copiado de ID de entidade de SAML do Olá portal do Azure.

    b. No Olá **sessão SAML no URL de destino** caixa, cole Olá único início de sessão no URL do serviço SAML copiado Olá portal do Azure.

    c. Agora abra Olá **XML de metadados** transferido acima de Olá portal do Azure e cópia Olá certficate na tag de Olá denominado **certificado X509**. Olá colar copiados valor para Olá **certificado de início de sessão único x509** caixa.

10. Clique em **guardar alterações**.

11. Depois destas definições, necessita de toosend Olá **nome de domínio** (por exemplo **contoso.com**) através do qual está a iniciar sessão em Procore toohello [equipa de suporte Procore](https://support.procore.com/) quais serão Ative a SSO federado desse domínio.

<!--### Next steps

tooensure users can sign-in tooProcore SSO after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooProcore SSO in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste no portal de gestão do Azure de Olá chamado Britta Simon.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal de gestão do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. Aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores** lista de Olá toodisplay de utilizadores.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. Na parte superior de Olá da caixa de diálogo Olá clique **adicionar** tooopen Olá **utilizador** caixa de diálogo.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-procore-sso-test-user"></a>Criar um utilizador de teste de Procore SSO

Siga Olá abaixo passos toocreate um utilizador de teste Procore no seu lado.

1. Site de empresa procore de tooyour de início de sessão como administrador.  

2. Na lista de caixa de ferramentas de Olá pendente, clique em **diretório** página de diretório do tooopen Olá da empresa.

    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. Clique em **adicionar uma pessoa** opção formulário de Olá tooopen e introduza efetuar os seguintes opções -

    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    a. No Olá **nome próprio** caixa de texto, nome do próprio do utilizador do tipo como **Britta**.

    b. No Olá **Apelido** caixa de texto, apelido do utilizador do tipo como **Simon**.

    c. No Olá **endereço de correio eletrónico** como endereço de correio eletrónico do utilizador do tipo de caixa de texto,  **BrittaSimon@contoso.com** .

    d. Selecione **permissão modelo** como **aplicar o modelo de permissão mais tarde**.

    e. Clique em **Criar**.

4. Verifique e atualizar os detalhes de Olá para Olá recentemente adicionadas contacto.

    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. Clique em **guardar e enviar Invitiation** (se for necessário um convite através de correio) ou **guardar** (guardar diretamente) registo de utilizador de Olá toocomplete.
    
    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo tooProcore respetivo acesso SSO.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooProcore SSO, execute Olá os seguintes passos:**

1. No portal de gestão do Azure de Olá, abra a vista de aplicações de Olá e, em seguida, navegue até a vista de diretório toohello e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **Procore SSO**.

    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Se pretender testar as definições de início de sessão único, abra o painel de acesso. Para obter mais detalhes sobre o painel de acesso, consulte [introdução ao painel de acesso](https://msdn.microsoft.com/library/dn308586). Ao clicar em mosaico de Procore SSO Olá no painel de acesso de Olá, deve obter a aplicação de Procore SSO tooyour automaticamente com sessão iniciada.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

