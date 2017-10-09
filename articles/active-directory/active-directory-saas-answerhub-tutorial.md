---
title: "Tutorial: Integração do Azure Active Directory com AnswerHub | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e AnswerHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 90b530da31abe7e6f18bfa2c5409f8ff1d4f1063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a>Tutorial: Integração do Azure Active Directory com AnswerHub

Neste tutorial, saiba como toointegrate AnswerHub com o Azure Active Directory (Azure AD).

Integrar AnswerHub com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooAnswerHub
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooAnswerHub (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com AnswerHub tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um AnswerHub-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar AnswerHub da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-answerhub-from-hello-gallery"></a>Adicionar AnswerHub da Galeria de Olá
tooconfigure Olá integração de AnswerHub com o Azure AD, é necessário tooadd AnswerHub Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd AnswerHub da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **AnswerHub**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_search.png)

5. No painel de resultados de Olá, selecione **AnswerHub**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com AnswerHub com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá AnswerHub é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá AnswerHub tem toobe estabelecida.

No AnswerHub, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com AnswerHub, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste AnswerHub](#creating-an-answerhub-test-user)**  -toohave um homólogo de Britta Simon no AnswerHub é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação AnswerHub.

**tooconfigure do Azure AD-início de sessão único com AnswerHub, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **AnswerHub** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_samlbase.png)

3. No Olá **AnswerHub domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_url.png)

    a. No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company>.answerhub.com`

    b. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company>.answerhub.com`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualizar estes valores com Olá real URL de início de sessão e o identificador. Contacte [equipa de suporte de cliente AnswerHub](mailto:success@answerhub.com) tooget estes valores. 
 
4. No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-answerhub-tutorial/tutorial_general_400.png)

6. No Olá **AnswerHub configuração** secção, clique em **configurar AnswerHub** tooopen **configurar início de sessão** janela. Olá cópia **Sign-Out URL e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_configure.png) 

7. Numa janela do browser web diferente, inicie sessão no site da sua empresa AnswerHub como administrador.
   
    >[!NOTE]
    >Se precisar de ajuda para configurar AnswerHub, contacte [equipa de suporte do AnswerHub](mailto:success@answerhub.com.).
   
8. Aceda demasiado**administração**.

9. Clique em Olá **utilizador e grupo** separador.

10. No painel de navegação de Olá no Olá left lado, nos Olá **definições de redes sociais** secção, clique em **configuração SAML**.

11. Clique em **IDP configuração** separador.

12. No Olá **IDP configuração** separador, execute Olá os seguintes passos:

     ![A configuração SAML](./media/active-directory-saas-answerhub-tutorial/ic785172.png "configuração SAML")  
  
     a. No **URL de início de sessão do IDP** caixa de texto, colar **único início de sessão no URL do serviço SAML** que copiou do portal do Azure.
  
     b. No **URL de fim de sessão do IDP** caixa de texto, colar **Sign-Out URL** valor que copiou do portal do Azure.
     
     c. No **formato do identificador de nome de IDP** caixa de texto, introduza o utilizador Olá identificador valor mesmo como seleccionado no portal do Azure no **atributos de utilizador** secção.
  
     d. Clique em **chaves e certificados**.

13. No separador de chaves e certificados de Olá, execute Olá os seguintes passos:
    
     ![As chaves e certificados](./media/active-directory-saas-answerhub-tutorial/ic785173.png "chaves e certificados")  
 
     a. Abra o seu certificado codificado de base-64 que transferiu a partir do portal do Azure no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência, e, em seguida, cole-toohello **chave pública do IDP (x 509 formato)** caixa de texto.
  
     b. Clique em **Guardar**.

14. No Olá **IDP configuração** separador, clique em **guardar**.

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-an-answerhub-test-user"></a>Criar um utilizador de teste AnswerHub

tooenable do Azure AD os utilizadores toolog no tooAnswerHub, estes têm de ser aprovisionados para AnswerHub.  
No caso de Olá da AnswerHub, o aprovisionamento é uma tarefa manual.

**tooprovision uma conta de utilizador, execute Olá os seguintes passos:**

1. Inicie sessão no tooyour **AnswerHub** site da empresa como administrador.

2. Aceda demasiado**administração**.

3. Clique em Olá **utilizadores e grupos** separador.

4. No painel de navegação de Olá no Olá left lado, nos Olá **gerir utilizadores** secção, clique em **criar ou importar utilizadores**.
   
   ![Utilizadores e grupos](./media/active-directory-saas-answerhub-tutorial/ic785175.png "utilizadores e grupos")

5. Olá tipo **endereço de correio eletrónico**, **Username** e **palavra-passe** de um Azure válido conta do Active Directory que pretende tooprovision Olá relacionadas com caixas de texto e, em seguida, clique em  **Guardar**.

>[!NOTE]
>Pode utilizar quaisquer outras AnswerHub utilizador conta criação ferramentas ou APIs fornecidas pelo AnswerHub tooprovision contas de utilizador do AAD.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooAnswerHub.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooAnswerHub, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **AnswerHub**.

    ![Configurar o início de sessão único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar em mosaico de AnswerHub Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour AnswerHub aplicação.
Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_203.png

