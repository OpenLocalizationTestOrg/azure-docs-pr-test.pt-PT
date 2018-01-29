---
title: "Tutorial: Integração do Azure Active Directory com TeamSeer | Microsoft Docs"
description: "Saiba como configurar o início de sessão entre o Azure Active Directory e TeamSeer."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: b67b2e22d1b2b13ab0103d00ba6c1e62b2fdd17b
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a>Tutorial: Integração do Azure Active Directory com TeamSeer

Neste tutorial, irá aprender a integrar TeamSeer com o Azure Active Directory (Azure AD).

Integrar TeamSeer com o Azure AD fornece as seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso ao TeamSeer
- Pode permitir que os utilizadores automaticamente obter com sessão iniciada para TeamSeer (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - portal do Azure

Se pretender saber mais detalhes sobre a integração de aplicações SaaS com o Azure AD, consulte o artigo [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com TeamSeer, terá dos seguintes itens:

- Uma subscrição do Azure AD
- Um TeamSeer início de sessão único subscrição ativado

> [!NOTE]
> Para testar os passos neste tutorial, não recomendamos a utilização num ambiente de produção.

Para testar os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar TeamSeer a partir da Galeria
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-teamseer-from-the-gallery"></a>Adicionar TeamSeer a partir da Galeria
Para configurar a integração de TeamSeer no Azure AD, terá de adicionar TeamSeer a partir da Galeria à sua lista de aplicações SaaS geridas.

**Para adicionar TeamSeer a partir da galeria, execute os seguintes passos:**

1. No  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue para **aplicações empresariais**. Em seguida, aceda a **todas as aplicações**.

    ![Aplicações][2]
    
3. Para adicionar a nova aplicação, clique em **nova aplicação** botão no topo da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa, escreva **TeamSeer**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_search.png)

5. No painel de resultados, selecione **TeamSeer**e, em seguida, clique em **adicionar** botão para adicionar a aplicação.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com TeamSeer com base num utilizador de teste chamado "Britta Simon."

Para início de sessão trabalhar, do Azure AD tem de saber o que o utilizador homólogo no TeamSeer é um utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionado no TeamSeer tem de ser estabelecida.

No TeamSeer, atribua o valor do **nome de utilizador** no Azure AD como o valor a **Username** para estabelecer a relação de ligação.

Para configurar e testar o Azure AD-início de sessão único com TeamSeer, tem de concluir os blocos modulares seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  - para permitir aos utilizadores utilizar esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  - para testar o Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste TeamSeer](#creating-a-teamseer-test-user)**  - para ter um homólogo de Britta Simon TeamSeer que está ligada a representação do Azure AD do utilizador.
4. **[Atribuir o utilizador de teste do Azure AD](#assigning-the-azure-ad-test-user)**  - para ativar Britta Simon utilizar o Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  - para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD início de sessão no portal do Azure e configurar o início de sessão único na sua aplicação TeamSeer.

**Para configurar o Azure AD-início de sessão único com TeamSeer, execute os seguintes passos:**

1. No portal do Azure, no **TeamSeer** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** para ativar o início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_samlbase.png)

3. No **TeamSeer domínio e os URLs** secção, execute os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_url.png)

     No **URL de início de sessão** caixa de texto, escreva um URL a utilizar o padrão do seguinte:`https://www.teamseer.com/<companyid>`

    > [!NOTE] 
    > O valor não é real. Atualize o valor com o URL de início de sessão real. Contacte [equipa de suporte de cliente TeamSeer](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) para obter o valor. 
 
4. No **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-teamseer-tutorial/tutorial_general_400.png)

6. No **TeamSeer configuração** secção, clique em **configurar TeamSeer** para abrir **configurar início de sessão** janela. Copiar o **único início de sessão no URL do serviço SAML** do **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_configure.png)

7. Numa janela do browser web diferente, inicie sessão no site da sua empresa TeamSeer como administrador.

8. Aceda a **HR Admin**.
   
    ![Administração de RH](./media/active-directory-saas-teamseer-tutorial/ic789634.png "Admin de RH")

9. Clique em **configuração**.
   
    ![A configuração](./media/active-directory-saas-teamseer-tutorial/ic789635.png "programa de configuração")

10. Clique em **configurar informações de fornecedor SAML**.
   
    ![Definições de SAML](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML definições")

11. Na seção de detalhes do fornecedor SAML, execute os seguintes passos:
   
    ![Definições de SAML](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML definições")   

    a. Colar o **URL Single Sign-On serviço** valor para o **URL** caixa de texto.
          
    b. Abra o certificado codificado base-64 no bloco de notas, copiar o conteúdo do mesmo para a sua área de transferência e, em seguida, cole-os para o **certificado público IdP** caixa de texto.

12. Para concluir a configuração do fornecedor SAML, execute os seguintes passos:
    
    ![Definições de SAML](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML definições") 

    a. No **endereços de E-Mail de teste**, escreva o endereço de e-mail do utilizador de teste. 
  
    b. No **emissor** caixa de texto, escreva o URL do emissor do fornecedor de serviço. 
  
    c. Clique em **Guardar**.

> [!TIP]
> Pode agora ler estas instruções dentro de uma versão concisa o [portal do Azure](https://portal.azure.com), enquanto estiver a configurar a aplicação!  Depois de adicionar esta aplicação a partir do **do Active Directory > aplicações da empresa** secção, basta clicar no **Single Sign-On** separador e aceder à documentação do embedded através de **configuração** secção na parte inferior. Pode ler mais sobre a funcionalidade de documentação incorporados aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
O objetivo desta secção consiste em criar um utilizador de teste no portal do Azure chamado Britta Simon.

![Criar utilizador do Azure AD][100]

**Para criar um utilizador de teste no Azure AD, execute os seguintes passos:**

1. No **portal do Azure**, no painel de navegação esquerdo, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_01.png) 

2. Para apresentar a lista de utilizadores, aceda a **utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_02.png) 

3. Para abrir o **utilizador** caixa de diálogo, clique em **adicionar** na parte superior da caixa de diálogo.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_03.png) 

4. No **utilizador** diálogo página, execute os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_04.png) 

    a. No **nome** caixa de texto, tipo **BrittaSimon**.

    b. No **nome de utilizador** caixa de texto, tipo de **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor da **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-teamseer-test-user"></a>Criar um utilizador de teste TeamSeer

Para permitir que os utilizadores do Azure AD iniciem sessão nos TeamSeer, estes têm de ser aprovisionados para ShiftPlanning. No caso de TeamSeer, o aprovisionamento é uma tarefa manual.

**Para Aprovisionar uma conta de utilizador, execute os seguintes passos:**

1. Inicie sessão no seu **TeamSeer** site da empresa como administrador.

2. Execute os seguintes passos:
   
    ![Administração de RH](./media/active-directory-saas-teamseer-tutorial/ic789640.png "Admin de RH")  
 
    a. Aceda a **HR Admin \> utilizadores**.
  
    b. Clique em **executar o Assistente do novo utilizador**.

3. No **detalhes de utilizador** secção, execute os seguintes passos:
   
    ![Detalhes de utilizador](./media/active-directory-saas-teamseer-tutorial/ic789641.png "detalhes de utilizador")

    a. Tipo de **nome próprio**, **Apelido**, **nome de utilizador (endereço de correio eletrónico)** de uma conta válida do AAD, pretende aprovisionar para caixas de texto relacionadas.
  
    b. Clique em **Seguinte**.

4. Siga o ecrã instruções para adicionar um novo utilizador e clique em **concluir**.

>[!NOTE]
>Pode utilizar quaisquer outras TeamSeer utilizador conta criação ferramentas ou APIs fornecidas pelo TeamSeer aprovisionar contas de utilizador do Azure AD. 

### <a name="assigning-the-azure-ad-test-user"></a>Atribuir o utilizador de teste do Azure AD

Nesta secção, vai ativar Britta Simon utilizar o Azure-início de sessão único, concedendo acesso para TeamSeer.

![Atribua o utilizador][200] 

**Para atribuir Britta Simon a TeamSeer, execute os seguintes passos:**

1. No portal do Azure, abra a vista de aplicações e, em seguida, navegue para a vista de diretório e aceda a **aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações, selecione **TeamSeer**.

    ![Configurar o início de sessão único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_app.png) 

3. No menu à esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista utilizadores.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Se pretender testar as definições de início de sessão único, abra o painel de acesso. Para obter mais detalhes sobre o painel de acesso, consulte [introdução ao painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicações SaaS com o Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_203.png

