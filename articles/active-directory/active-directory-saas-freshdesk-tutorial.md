---
title: "Tutorial: Integração do Azure Active Directory com FreshDesk | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e FreshDesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 577a5eb6d9b1bc03030a2b47f63d375869c903bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a>Tutorial: Integração do Azure Active Directory com FreshDesk

Neste tutorial, saiba como toointegrate FreshDesk com o Azure Active Directory (Azure AD).

Integrar FreshDesk com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooFreshDesk
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooFreshDesk (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - portal de gestão do Azure de Olá

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com FreshDesk tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um FreshDesk início de sessão único subscrição ativado

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar FreshDesk da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-freshdesk-from-hello-gallery"></a>Adicionar FreshDesk da Galeria de Olá
tooconfigure Olá integração de FreshDesk com o Azure AD, é necessário tooadd FreshDesk Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd FreshDesk da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[Azure Management Portal](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. Clique em **adicionar** botão na parte superior de Olá da caixa de diálogo Olá.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **FreshDesk**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. No painel de resultados de Olá, selecione **FreshDesk**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com FreshDesk com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá FreshDesk é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá FreshDesk tem toobe estabelecida.

Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no FreshDesk.

tooconfigure e teste do Azure AD-início de sessão único com FreshDesk, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste FreshDesk](#creating-a-freshdesk-test-user)**  -toohave um homólogo de Britta Simon no FreshDesk é-lhe representação toohello ligado do Azure AD.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD início de sessão no portal de gestão do Azure Olá e configurar o início de sessão único na sua aplicação FreshDesk.

**tooconfigure do Azure AD-início de sessão único com FreshDesk, execute Olá os seguintes passos:**

1. No portal de gestão do Azure de Olá, no Olá **FreshDesk** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, como **modo** selecione **baseados em SAML início de sessão** tooenable início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. No Olá **FreshDesk domínio e os URLs** secção, introduza Olá **URL de início de sessão** como: `https://<tenant-name>.freshdesk.com` ou qualquer outro valor Freshdesk tem sugeridos.

    ![Configurar o início de sessão único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > Tenha em atenção que isto não é o valor real. Tem de atualizar o valor com o URL de início de sessão real. Contacte [equipa de suporte de cliente FreshDesk](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) para obter este valor.  

4. No Olá **certificado de assinatura de SAML** secção, clique em **certificado** e, em seguida, guarde o certificado de Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. No Olá **FreshDesk configuração** secção, clique em **configurar FreshDesk** janela tooopen configurar início de sessão. Copiar Olá único início de sessão no URL do serviço SAML e o URL de Sign-Out de Olá **referência rápida** secção.

    ![Configurar o início de sessão único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. Numa janela do browser web diferente, inicie sessão no site da sua empresa Freshdesk como administrador.

8. No menu de Olá na parte superior do Olá, clique em **Admin**.
   
   ![Administração](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")

9. No Olá **definições gerais** separador, clique em **segurança**.
   
   ![Segurança](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "segurança")

10. No Olá **segurança** secção, execute Olá os seguintes passos:
   
    ![Início de sessão único](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "início de sessão único")
   
    a. Para **único início de sessão (SSO)**, selecione **no**.

    b. Selecione **SAML SSO**.

    c. Olá tipo **único início de sessão no URL do serviço SAML** copiados a partir do portal do Azure para Olá **URL de início de sessão SAML** caixa de texto.

    d. Olá tipo **Sign-Out URL** copiados a partir do portal do Azure para Olá **URL de fim de sessão** caixa de texto.

    e. Olá cópia **Thumbprint** valor do certificado de Olá transferido a partir do portal do Azure e cole-o Olá **impressão digital do certificado de segurança** caixa de texto.  
 
    >[!TIP]
    >Para obter mais detalhes, consulte [como tooretrieve valor do thumbprint do certificado](http://youtu.be/YKQF266SAxI). 
    
    f. Clique em **Guardar**.


### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste no portal de gestão do Azure de Olá chamado Britta Simon.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal de gestão do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. Aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores** lista de Olá toodisplay de utilizadores.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. Na parte superior de Olá da caixa de diálogo Olá clique **adicionar** tooopen Olá **utilizador** caixa de diálogo.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-freshdesk-test-user"></a>Criar um utilizador de teste FreshDesk

Na ordem tooenable do Azure AD os utilizadores toolog para FreshDesk, têm de ser aprovisionados para FreshDesk.  
No caso de Olá da FreshDesk, o aprovisionamento é uma tarefa manual.

**executar de contas de utilizador, tooprovision Olá os seguintes passos:**

1. Inicie sessão no tooyour **Freshdesk** inquilino.
2. No menu de Olá na parte superior do Olá, clique em **Admin**.
   
   ![Administração](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")

3. No Olá **definições gerais** separador, clique em **agentes**.
   
   ![Agentes](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "agentes")

4. Clique em **novo agente**.
   
    ![Novo agente](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "novo agente")

5. Na caixa de diálogo de informações de agentes Olá, execute Olá os seguintes passos:
   
   ![Informações de agentes](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "informações de agentes")
   
   a. No Olá **nome completo** caixa de texto, nome do tipo Olá da conta de Olá do Azure AD que pretende tooprovision.

   b. No Olá **E-Mail** caixa de texto, Olá de tipo do Azure AD endereço de e-mail da conta de Olá do Azure AD que pretende tooprovision.

   c. No Olá **título** caixa de texto, tipo Olá título da conta de Olá do Azure AD que pretende tooprovision.

   d. Selecione **função agentes**e, em seguida, clique em **atribuir**.
       
   e. Clique em **Guardar**.     
   
    >[!NOTE]
    >titular da conta do Olá do Azure AD irá receber uma mensagem de e-mail que inclui uma conta de Olá tooconfirm ligação antes de ser ativado. 
    > 
    
    >[!NOTE]
    >Pode utilizar quaisquer outras Freshdesk utilizador conta criação ferramentas ou APIs fornecidas pelo Freshdesk tooprovision contas de utilizador do AAD. tooFreshDesk.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo utras tooBox de acesso.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooFreshDesk, execute Olá os seguintes passos:**

1. No portal de gestão do Azure de Olá, abra a vista de aplicações de Olá e, em seguida, navegue até a vista de diretório toohello e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **FreshDesk**.

    ![Configurar o início de sessão único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar em mosaico de FreshDesk Olá no painel de acesso de Olá, deve obter início de sessão página tooget com sessão iniciada tooyour FreshDesk aplicação.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

