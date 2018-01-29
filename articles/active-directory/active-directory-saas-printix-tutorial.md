---
title: "Tutorial: Integração do Azure Active Directory com Printix | Microsoft Docs"
description: "Saiba como configurar o início de sessão entre o Azure Active Directory e Printix."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 4aea7320-b2d5-49e0-9b63-aeaff0f6fe66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 3b04388d3d91d9fb1ac38988071ebb5ab00366ee
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-printix"></a>Tutorial: Integração do Azure Active Directory com Printix

Neste tutorial, irá aprender a integrar Printix com o Azure Active Directory (Azure AD).

Integrar Printix com o Azure AD fornece as seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso ao Printix
- Pode permitir que os utilizadores automaticamente obter com sessão iniciada para Printix (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - portal do Azure

Se pretender saber mais detalhes sobre a integração de aplicações SaaS com o Azure AD, consulte o artigo [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com Printix, terá dos seguintes itens:

- Uma subscrição do Azure AD
- Um Printix-início de sessão único ativada subscrição

> [!NOTE]
> Para testar os passos neste tutorial, não recomendamos a utilização num ambiente de produção.

Para testar os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar Printix a partir da Galeria
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-printix-from-the-gallery"></a>Adicionar Printix a partir da Galeria
Para configurar a integração de Printix com o Azure AD, terá de adicionar Printix a partir da Galeria à sua lista de aplicações SaaS geridas.

**Para adicionar Printix a partir da galeria, execute os seguintes passos:**

1. No  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue para **aplicações empresariais**. Em seguida, aceda a **todas as aplicações**.

    ![Aplicações][2]
    
3. Para adicionar a nova aplicação, clique em **nova aplicação** botão no topo da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa, escreva **Printix**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-printix-tutorial/tutorial_printix_search.png)

5. No painel de resultados, selecione **Printix**e, em seguida, clique em **adicionar** botão para adicionar a aplicação.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-printix-tutorial/tutorial_printix_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com Printix com base num utilizador de teste chamado "Britta Simon".

Para início de sessão trabalhar, do Azure AD tem de saber o que o utilizador homólogo no Printix é um utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionado no Printix tem de ser estabelecida.

No Printix, atribua o valor do **nome de utilizador** no Azure AD como o valor a **Username** para estabelecer a relação de ligação.

Para configurar e testar o Azure AD-início de sessão único com Printix, tem de concluir os blocos modulares seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  - para permitir aos utilizadores utilizar esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  - para testar o Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Printix](#creating-a-printix-test-user)**  - para ter um homólogo de Britta Simon Printix que está ligada a representação do Azure AD do utilizador.
4. **[Atribuir o utilizador de teste do Azure AD](#assigning-the-azure-ad-test-user)**  - para ativar Britta Simon utilizar o Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  - para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD início de sessão no portal do Azure e configurar o início de sessão único na sua aplicação Printix.

**Para configurar o Azure AD-início de sessão único com Printix, execute os seguintes passos:**

1. No portal do Azure, no **Printix** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** para ativar o início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-printix-tutorial/tutorial_printix_samlbase.png)

3. No **Printix domínio e os URLs** secção, execute os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-printix-tutorial/tutorial_printix_url.png)

    No **URL de início de sessão** caixa de texto, escreva um URL a utilizar o padrão do seguinte:`https://<subdomain>.printix.net`

    > [!NOTE] 
    > O valor não é real. Atualize o valor com o URL de início de sessão real. Contacte [equipa de suporte de cliente Printix](mailto:support@printix.net) para obter o valor. 
 
4. No **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-printix-tutorial/tutorial_printix_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-printix-tutorial/tutorial_general_400.png)

6. Início de sessão no seu inquilino Printix como administrador.

7. No menu na parte superior, clique no ícone no canto superior direito e selecione "**autenticação**".
   
    ![Configurar o início de sessão único](./media/active-directory-saas-printix-tutorial/tutorial_printix_06.png)

8. No **configuração** separador, selecione **autenticação ativar o Azure/Office 365**
   
    ![Configurar o início de sessão único](./media/active-directory-saas-printix-tutorial/tutorial_printix_07.png)

9. No **Azure** separador, introduza o URL de metadados de Federação para a caixa de texto de "**documento de metadados de Federação**". 

    Anexar o ficheiro xml de metadados que transferiu a partir do Azure AD para [equipa de suporte de Printix](mailto:support@printix.net). Em seguida, carregue o ficheiro xml e fornecer um URL de metadados de Federação.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-printix-tutorial/tutorial_printix_08.png)
   
10. Clique em de "**testar**"botão e clique em"**OK**" botão se o teste foi concluída com êxito.
   
     Página do Azure active directory irá mostrar depois de clicar no **testar** botão. "O teste foi concluída com êxito" aqui significa que depois de introduzir as credenciais da sua conta de teste do Azure irá destaque se uma mensagem "definições testado OK". Em seguida, clique o **OK** botão.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-printix-tutorial/tutorial_printix_09.png)

11. Clique em de **guardar** botão no "**autenticação**" página.


> [!TIP]
> Pode agora ler estas instruções dentro de uma versão concisa o [portal do Azure](https://portal.azure.com), enquanto estiver a configurar a aplicação!  Depois de adicionar esta aplicação a partir do **do Active Directory > aplicações da empresa** secção, basta clicar no **Single Sign-On** separador e aceder à documentação do embedded através de **configuração** secção na parte inferior. Pode ler mais sobre a funcionalidade de documentação incorporados aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
O objetivo desta secção consiste em criar um utilizador de teste no portal do Azure chamado Britta Simon.

![Criar utilizador do Azure AD][100]

**Para criar um utilizador de teste no Azure AD, execute os seguintes passos:**

1. No **portal do Azure**, no painel de navegação esquerdo, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_01.png) 

2. Para apresentar a lista de utilizadores, aceda a **utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_02.png) 

3. Para abrir o **utilizador** caixa de diálogo, clique em **adicionar** na parte superior da caixa de diálogo.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_03.png) 

4. No **utilizador** diálogo página, execute os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_04.png) 

    a. No **nome** caixa de texto, tipo **BrittaSimon**.

    b. No **nome de utilizador** caixa de texto, tipo de **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor da **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-printix-test-user"></a>Criar um utilizador de teste Printix

O objetivo desta secção consiste em criar um utilizador chamado Britta Simon Printix. Printix suporta o aprovisionamento de just-in-time, que está por predefinição, ativada.

Não há nenhum item de ação para si nesta secção. Um novo utilizador é criado durante a tentativa de aceder Printix se não existir ainda. 

> [!NOTE]
> Se precisar de criar manualmente um utilizador, terá de contactar o [equipa de suporte de Printix](mailto:support@printix.net).
> 

### <a name="assigning-the-azure-ad-test-user"></a>Atribuir o utilizador de teste do Azure AD

Nesta secção, vai ativar Britta Simon utilizar o Azure-início de sessão único, concedendo acesso para Printix.

![Atribua o utilizador][200] 

**Para atribuir Britta Simon a Printix, execute os seguintes passos:**

1. No portal do Azure, abra a vista de aplicações e, em seguida, navegue para a vista de diretório e aceda a **aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações, selecione **Printix**.

    ![Configurar o início de sessão único](./media/active-directory-saas-printix-tutorial/tutorial_printix_app.png) 

3. No menu à esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista utilizadores.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão através do painel de acesso.

Quando clica no mosaico Printix no painel de acesso, deve obter automaticamente com sessão iniciada para a aplicação de Printix.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicações SaaS com o Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-printix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-printix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-printix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-printix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-printix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-printix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-printix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-printix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-printix-tutorial/tutorial_general_203.png

