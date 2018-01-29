---
title: "Tutorial: Integração do Azure Active Directory com eKincare | Microsoft Docs"
description: "Saiba como configurar o início de sessão entre o Azure Active Directory e eKincare."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 57f56d14-83cf-4cbb-b342-fac4fc60078f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 6d85f8b30fb3e89f62a71572f0ff650c06c6d572
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ekincare"></a>Tutorial: Integração do Azure Active Directory com eKincare

Neste tutorial, irá aprender a integrar eKincare com o Azure Active Directory (Azure AD).

Integrar eKincare com o Azure AD fornece as seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso ao eKincare
- Pode permitir que os utilizadores automaticamente obter com sessão iniciada para eKincare (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - portal do Azure

Se pretender saber mais detalhes sobre a integração de aplicações SaaS com o Azure AD, consulte o artigo [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com eKincare, terá dos seguintes itens:

- Uma subscrição do Azure AD
- Um eKincare início de sessão único subscrição ativado

> [!NOTE]
> Para testar os passos neste tutorial, não recomendamos a utilização num ambiente de produção.

Para testar os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar eKincare a partir da Galeria
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-ekincare-from-the-gallery"></a>Adicionar eKincare a partir da Galeria
Para configurar a integração de eKincare com o Azure AD, terá de adicionar eKincare a partir da Galeria à sua lista de aplicações SaaS geridas.

**Para adicionar eKincare a partir da galeria, execute os seguintes passos:**

1. No  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue para **aplicações empresariais**. Em seguida, aceda a **todas as aplicações**.

    ![Aplicações][2]
    
3. Para adicionar a nova aplicação, clique em **nova aplicação** botão no topo da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa, escreva **eKincare**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_search.png)

5. No painel de resultados, selecione **eKincare**e, em seguida, clique em **adicionar** botão para adicionar a aplicação.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com eKincare com base num utilizador de teste chamado "Britta Simon."

Para início de sessão trabalhar, do Azure AD tem de saber o que o utilizador homólogo no eKincare é um utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionado no eKincare tem de ser estabelecida.

No eKincare, atribua o valor do **nome de utilizador** no Azure AD como o valor a **Username** para estabelecer a relação de ligação.

Para configurar e testar o Azure AD-início de sessão único com eKincare, tem de concluir os blocos modulares seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  - para permitir aos utilizadores utilizar esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  - para testar o Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste eKincare](#creating-a-ekincare-test-user)**  - para ter um homólogo de Britta Simon no eKincare que está ligada a representação do Azure AD do utilizador.
4. **[Atribuir o utilizador de teste do Azure AD](#assigning-the-azure-ad-test-user)**  - para ativar Britta Simon utilizar o Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  - para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD início de sessão no portal do Azure e configurar o início de sessão único na sua aplicação eKincare.

**Para configurar o Azure AD-início de sessão único com eKincare, execute os seguintes passos:**

1. No portal do Azure, no **eKincare** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** para ativar o início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_samlbase.png)

3. No **eKincare domínios e URLs** secção, execute os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_url.png)

    a. No **identificador** caixa de texto, escreva um URL a utilizar o padrão do seguinte:`https://<instancename>.ekincare.com/`

    b. No **URL de resposta** caixa de texto, escreva um URL a utilizar o padrão do seguinte:`https://<instancename>.ekincare.com/hul/saml`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualize estes valores com o identificador e o URL de resposta real. Contacte [equipa de suporte de eKincare](mailto:tech@ekincare.com) para obter estes valores.
 
4. aplicação de eKincare espera as asserções de SAML num formato específico. Configure as seguintes afirmações para esta aplicação. Pode gerir os valores destes atributos a partir de "**atributos de utilizador**" secção na página de integração de aplicações. A seguinte captura de ecrã mostra um exemplo para esta configuração.

    O nome de afirmação será sempre **"campo IDdeEmpregado"** e o valor que podemos ter mapeado para user.extensionattribute1, que contém o campo IDdeEmpregado do utilizador. Nome revertidos das outras duas afirmações **"organizationid"** e **"organizationname"** será sempre mesmo e os respetivos valores contém os detalhes da organização do utilizador, respetivamente.
    
    ![Configurar o início de sessão único](./media/active-directory-saas-ekincare-tutorial/attribute.png)
    
5. No **atributos de utilizador** secção no **de sessão único-** caixa de diálogo, configurar atributos token SAML, conforme mostrado na imagem acima e execute os seguintes passos:
    
    | Nome do Atributo | Valor do Atributo |
    | ---------------| --------------- |    
    | Campo IDdeEmpregado | *User.extensionattribute1* |
    | OrganizationId | *"uniquevalue"* |
    | OrganizationName | *User.companyname* |

    a. Clique em **adicionar atributo** para abrir o **adicionar atributo** caixa de diálogo.

    ![Configurar o início de sessão único](./media/active-directory-saas-ekincare-tutorial/04.png)

    ![Configurar o início de sessão único](./media/active-directory-saas-ekincare-tutorial/05.png)
    
    b. No **nome** caixa de texto, escreva o nome de atributo apresentado para essa linha.
    
    c. Do **valor** lista, digite o valor de atributo apresentado para essa linha.
    
    d. Clique em **Ok**

6. No **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_certificate.png) 

7. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-ekincare-tutorial/tutorial_general_400.png)

8. Para configurar o início de sessão único em **eKincare** lado, terá de enviar o transferido **XML de metadados** para [equipa de suporte de eKincare](mailto:tech@ekincare.com). Se definir esta definição para que a ligação de SAML SSO corretamente em ambos os lados.

> [!TIP]
> Pode agora ler estas instruções dentro de uma versão concisa o [portal do Azure](https://portal.azure.com), enquanto estiver a configurar a aplicação!  Depois de adicionar esta aplicação a partir do **do Active Directory > aplicações da empresa** secção, basta clicar no **Single Sign-On** separador e aceder à documentação do embedded através de **configuração** secção na parte inferior. Pode ler mais sobre a funcionalidade de documentação incorporados aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
O objetivo desta secção consiste em criar um utilizador de teste no portal do Azure chamado Britta Simon.

![Criar utilizador do Azure AD][100]

**Para criar um utilizador de teste no Azure AD, execute os seguintes passos:**

1. No **portal do Azure**, no painel de navegação esquerdo, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_01.png) 

2. Para apresentar a lista de utilizadores, aceda a **utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_02.png) 

3. Para abrir o **utilizador** caixa de diálogo, clique em **adicionar** na parte superior da caixa de diálogo.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_03.png) 

4. No **utilizador** diálogo página, execute os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_04.png) 

    a. No **nome** caixa de texto, tipo **BrittaSimon**.

    b. No **nome de utilizador** caixa de texto, tipo de **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor da **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-ekincare-test-user"></a>Criar um utilizador de teste eKincare

Aplicação suporta apenas no tempo de aprovisionamento de utilizador e de utilizadores de autenticação são criados automaticamente na aplicação.

### <a name="assigning-the-azure-ad-test-user"></a>Atribuir o utilizador de teste do Azure AD

Nesta secção, vai ativar Britta Simon utilizar o Azure-início de sessão único, concedendo acesso aos eKincare.

![Atribua o utilizador][200] 

**Para atribuir Britta Simon a eKincare, execute os seguintes passos:**

1. No portal do Azure, abra a vista de aplicações e, em seguida, navegue para a vista de diretório e aceda a **aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações, selecione **eKincare**.

    ![Configurar o início de sessão único](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_app.png) 

3. No menu à esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista utilizadores.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão através do painel de acesso.

Quando clica no mosaico eKincare no painel de acesso, deve obter automaticamente com sessão iniciada para a aplicação de eKincare.
Para mais informações sobre o painel de acesso, consulte [introdução ao painel de acesso](active-directory-saas-access-panel-introduction.md)

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicações SaaS com o Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_203.png

