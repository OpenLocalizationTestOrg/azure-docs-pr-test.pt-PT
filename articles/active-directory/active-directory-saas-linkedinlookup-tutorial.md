---
title: "Tutorial: Integração do Azure Active Directory com LinkedIn pesquisa | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e LinkedIn pesquisa."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: d79c34baa676391699e4b49806f16422fcfe73e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a>Tutorial: Integração do Azure Active Directory com LinkedIn pesquisa

Neste tutorial, saiba como toointegrate LinkedIn pesquisa no Azure Active Directory (Azure AD).

A integração de pesquisa de LinkedIn com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooLinkedIn pesquisa
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooLinkedIn pesquisa (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com LinkedIn pesquisa tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um pesquisa de LinkedIn início de sessão único subscrição ativado

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. A adição de pesquisa do LinkedIn da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-linkedin-lookup-from-hello-gallery"></a>A adição de pesquisa do LinkedIn da Galeria de Olá
tooconfigure Olá integração de pesquisa de LinkedIn com o Azure AD, é necessário tooadd LinkedIn pesquisa Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd pesquisa LinkedIn da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. Clique em **nova aplicação** botão na parte superior de Olá da nova aplicação tooadd da caixa de diálogo de Olá.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **LinkedIn pesquisa**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. No painel de resultados de Olá, selecione **LinkedIn pesquisa**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com LinkedIn pesquisa com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow qual o utilizador que homólogo Olá na pesquisa do LinkedIn é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá na pesquisa do LinkedIn tem toobe estabelecida.

Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** na pesquisa do LinkedIn.

tooconfigure e teste do Azure AD-início de sessão único com LinkedIn pesquisa, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste de pesquisa de LinkedIn](#creating-an-linkedin-lookup-test-user)**  -toohave um homólogo de Britta Simon na pesquisa de LinkedIn que é a representação de toohello ligado do Azure AD.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação de pesquisa de LinkedIn.

**tooconfigure do Azure AD-início de sessão único com LinkedIn pesquisa, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **LinkedIn pesquisa** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, em **modo** selecione **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. Numa janela do browser web diferente, início de sessão tooyour **LinkedIn pesquisa** Web site como um administrador.

4. No **Centro de contas**, clique em **definições globais** em **definições**. Além disso, selecione **pesquisa** na lista pendente de Olá.

    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. Clique em **ou clique aqui tooload e copiar campos individuais de formulário de Olá** e copie **Id de entidade** e **Url de acesso de consumidor da asserção (ACS)**

    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. No portal do Azure, em **LinkedIn pesquisa de domínio e os URLs** secção, execute os passos seguintes se quiser aplicação Olá tooconfigure de Olá **IDP** iniciada modo:

    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    a. No Olá **identificador** caixa de texto, introduza Olá **ID de entidade** copiados a partir do LinkedIn Portal 

    b. No Olá **URL de resposta** caixa de texto, introduza Olá **Url de acesso de consumidor da asserção (ACS)** copiados a partir do LinkedIn Portal

7. Verifique **Mostrar avançadas definições de URL**, se desejar aplicação Olá tooconfigure **SP** iniciada modo:

    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`
     
    > [!NOTE] 
    > Não se trata de valor real. utilizador Olá tem tooupdate estes valores com Olá real URL de início de sessão. Contacte [equipa de suporte de cliente de pesquisa do LinkedIn](https://business.LinkedIn.com/lookup) tooget este valor.

8. O **LinkedIn pesquisa** aplicação espera asserções de SAML Olá num formato específico. utilizador Olá tem a configuração de atributos de tokens de SAML mapeamentos toohello tooadd atributo personalizado. Olá seguinte captura de ecrã mostra um exemplo. Olá valor predefinido de **identificador de utilizador** é **user.userprincipalname** mas LinkedIn pesquisa espera este toobe mapeado com o endereço de correio eletrónico do utilizador Olá. Pode utilizar **user.mail** atributo da lista de Olá ou utilize o valor do atributo adequado Olá com base na configuração da sua organização. 

    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. No **atributos de utilizador** secção, clique em **ver e editar todos os outros atributos de utilizador** e defina os atributos de Olá. afirmações de quatro tooadd com o nome tem de utilizador de Olá **e-mail**, **departamento**, **firstname**, e **lastname** e valor de Olá é toobe mapeado com **user.mail**, **user.department**, **user.givenname**, e **user.surname** respetivamente

    | Nome do atributo | Valor do atributo |
    | --- | --- |
    | Correio eletrónico| User.Mail |    
    | Departamento| User.Department |
    | nome próprio| User.givenName |
    | Apelido| User.Surname |

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    a. Clique em **adicionar atributo** tooopen Olá **adicionar atributo** caixa de diálogo.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    b. No Olá **nome** caixa de texto, nome de atributo do tipo Olá mostrado para essa linha.
    
    c. De Olá **valor** lista, o valor de atributo do tipo Olá mostrado para essa linha.
    
    d. Clique em **Ok**

10. Efetuar Olá os seguintes passos no Olá **nome** atributo -

    a. Clique em Olá do Olá atributo tooopen **Editar atributo** janela.

    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    b. Eliminar o valor do URL de Olá da Olá **espaço de nomes**.
    
    c. Clique em **Ok** definição de Olá toosave.

10. No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro XML de Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. Aceda demasiado**definições de administrador do LinkedIn** secção. Ficheiro XML Olá de carregamento transferiu a partir do portal do Azure de Olá clicando Olá **ficheiro XML de carregar** opção.

    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. Clique em **no** tooenable SSO. Estado SSO é alterado de **não ligado** demasiado**ligado**

    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. Aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. Clique em **adicionar** tooopen Olá **utilizador** caixa de diálogo.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **Britta Simon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de Britta Simon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-an-linkedin-lookup-test-user"></a>Criar um utilizador de teste de pesquisa de LinkedIn

Aplicação de pesquisa ligado suporta apenas no tempo (JIT) de aprovisionamento de utilizador e de utilizadores de autenticação são criados na aplicação Olá automaticamente. Ativar **automaticamente atribuir licenças** tooassign um utilizador de toohello de licença.
   
   ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooLinkedIn pesquisa.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooLinkedIn pesquisa, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **LinkedIn pesquisa**.

    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.

    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar Olá LinkedIn pesquisa na peça de mosaico Olá painel de acesso, deve ser página tooOrganizational redirecionada onde tiver tooprovide detalhes da sua conta LinkedIn pessoais. -Liga a sua conta pessoal com a sua conta de negócio LinkedIn. 

Para mais informações sobre o painel de acesso, consulte [introdução ao painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png

