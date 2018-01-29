---
title: "Tutorial: Integração do Azure Active Directory com redes da Palo Alto - Admin IU | Microsoft Docs"
description: "Saiba como configurar o início de sessão entre o Azure Active Directory e redes da Palo Alto - UI de Admin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: a826eaec-15af-4c85-8855-8a3374d1efb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/01/2017
ms.author: jeedes
ms.openlocfilehash: 8e54630d97dee2388ffc9c8877faeac269df1609
ms.sourcegitcommit: 2a70752d0987585d480f374c3e2dba0cd5097880
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/19/2018
---
# <a name="tutorial-azure-active-directory-integration-with-palo-alto-networks---admin-ui"></a>Tutorial: Integração do Azure Active Directory com redes da Palo Alto - Admin IU

Neste tutorial, irá aprender a integrar redes da Palo Alto - UI de administrador no Azure Active Directory (Azure AD).

Integração da Palo Alto redes - UI de administração com o Azure AD fornece as seguintes vantagens:

- Pode controlar no Azure AD quem tem acesso às redes da Palo Alto - UI de Admin.
- Pode permitir que os utilizadores automaticamente obter com sessão iniciada para redes da Palo Alto - IU de Admin (Single Sign-On) com as respetivas contas do Azure AD.
- Pode gerir as contas numa localização central - portal do Azure.

Se pretender saber mais detalhes sobre a integração de aplicações SaaS com o Azure AD, consulte o artigo [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com redes da Palo Alto - Admin IU, terá dos seguintes itens:

- Uma subscrição do Azure AD
- Uma Firewall de próxima geração de redes da Palo Alto ou Panorama (gestão centralizada de sistema para as firewalls)

> [!NOTE]
> Para testar os passos neste tutorial, não recomendamos a utilização num ambiente de produção.

Para testar os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos modulares principais:

1. A adição da Palo Alto redes - Admin IU da galeria do
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-palo-alto-networks---admin-ui-from-the-gallery"></a>A adição da Palo Alto redes - Admin IU da galeria do
Para configurar a integração das redes da Palo Alto - UI de administração com o Azure AD, terá de adicionar redes da Palo Alto - Admin IU da Galeria à sua lista de aplicações SaaS geridas.

**Para adicionar redes da Palo Alto - Admin IU da galeria, execute os seguintes passos:**

1. No  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo, clique em **do Azure Active Directory** ícone. 

    ![O botão do Azure Active Directory][1]

2. Navegue para **aplicações empresariais**. Em seguida, aceda a **todas as aplicações**.

    ![O painel de aplicações da empresa][2]
    
3. Para adicionar a nova aplicação, clique em **nova aplicação** botão no topo da caixa de diálogo.

    ![O novo botão de aplicação][3]

4. Na caixa de pesquisa, escreva **redes da Palo Alto - Admin IU**, selecione **redes da Palo Alto - Admin IU** partir do painel de resultados, em seguida, clique em **adicionar** botão para adicionar a aplicação.

    ![Redes da Palo Alto - UI de administrador na lista de resultados](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_step4-add-from-the-gallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD-início de sessão único

Nesta secção, configure e teste do Azure AD-início de sessão único com redes da Palo Alto - UI de administração baseada num utilizador de teste chamado "Britta Simon".

Para início de sessão trabalhar, do Azure AD tem de saber o que o utilizador homólogo nas redes da Palo Alto - UI de Admin é um utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionado nas redes da Palo Alto - UI de administrador tem de ser estabelecida.

Nas redes da Palo Alto - Admin IU, atribua o valor do **nome de utilizador** no Azure AD como o valor a **Username** para estabelecer a relação de ligação.

Para configurar e testar o Azure AD-início de sessão único com redes da Palo Alto - IU de administrador, tem de concluir os blocos modulares seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  - para permitir aos utilizadores utilizar esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  - para testar o Azure AD-início de sessão único com Britta Simon.
3. **[Criar um redes da Palo Alto - utilizador de teste de IU de Admin](#create-a-palo-alto-networks---admin-ui-test-user)**  - para ter um homólogo de Britta Simon nas redes da Palo Alto - UI de administrador que está ligada a representação do Azure AD do utilizador.
4. **[Atribua o utilizador de teste do Azure AD](#assign-the-azure-ad-test-user)**  - para ativar Britta Simon utilizar o Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#test-single-sign-on)**  - para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD início de sessão no portal do Azure e configurar o início de sessão único nas suas redes da Palo Alto - a aplicação de IU de Admin.

**Para configurar o Azure AD-início de sessão único com redes da Palo Alto - Admin IU, execute os seguintes passos:**

1. No portal do Azure, no **redes da Palo Alto - Admin IU** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar a ligação de início de sessão único][4]

2. No **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** para ativar o início de sessão único.
 
    ![Caixa de diálogo de início de sessão único](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_paloaltoadmin_samlbase.png)

3. No **da Palo Alto redes - administrador de domínio de IU e URLs** secção, execute os seguintes passos:

    ![Redes da Palo Alto - administrador de domínio de IU e URLs único início de sessão informações](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_paloaltoadmin_url.png)

    a. No **URL de início de sessão** caixa de texto, escreva um URL a utilizar o padrão do seguinte:`https://<Customer Firewall FQDN>/php/login.php`

    b. No **identificador** caixa de texto, escreva um URL a utilizar o padrão do seguinte:`https://<Customer Firewall FQDN>/SAML20/SP`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualize estes valores com o URL de início de sessão e o identificador real. Contacte [redes da Palo Alto - equipa de suporte de cliente de IU de Admin](https://support.paloaltonetworks.com/support) para obter estes valores. 
 
4. Redes da Palo Alto - aplicações de IU de Admin espera as asserções de SAML num formato específico. Configure as seguintes afirmações para esta aplicação. Pode gerir os valores destes atributos a partir de "**atributos de utilizador**" secção na página de integração de aplicações. A seguinte captura de ecrã mostra um exemplo para este.
    
    ![Configurar o início de sessão único](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_paloaltoadmin_attribute.png)
    
5. No **atributos de utilizador** secção no **de sessão único-** caixa de diálogo, configurar atributos token SAML, conforme mostrado na imagem acima e execute os seguintes passos: tenha em atenção que os valores de atributo são apenas de exemplo mapa os valores adequados para o nome de utilizador e adminrole. Não há outro atributo opcional "accessdomain", que é utilizado para restringir o acesso de administrador para sistemas virtuais específicos na firewall.
        
    | Nome do Atributo | Valor do Atributo |
    | --- | --- |    
    | o nome de utilizador | user.userprincipalname |
    | adminrole | customadmin |

    a. Clique em **adicionar atributo** para abrir o **adicionar atributo** caixa de diálogo.

    ![Configurar o início de sessão único](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_attribute_04.png)

    ![Configurar o início de sessão único](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_attribute_05.png)
    
    b. No **nome** caixa de texto, escreva o nome de atributo apresentado para essa linha.
    
    c. Do **valor** lista, digite o valor de atributo apresentado para essa linha.
    
    d. Clique em **Ok**

    > [!NOTE]
    > Pode consultar os seguintes artigos para obter mais detalhes sobre os atributos.
    > 1. Perfil de função administrativa para a IU de Admin (adminrole): https://www.paloaltonetworks.com/documentation/80/pan-os/pan-os/firewall-administration/manage-firewall-administrators/configure-an-admin-role-profile
    > 2. Domínio de acesso do dispositivo para a IU de Admin (accessdomain): https://www.paloaltonetworks.com/documentation/80/pan-os/web-interface-help/device/device-access-domain

6. No **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados no seu computador.

    ![A hiperligação de transferência do certificado](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_paloaltoadmin_certificate.png) 

7. Clique em **guardar** botão.

    ![Configurar botão único início de sessão guardar](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_general_400.png)

8. Abra a IU da Firewall da Palo Alto redes Admin como um administrador na outra janela do browser.

9. Clique em **dispositivo**.

    ![Configurar da Palo Alto-início de sessão único](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_paloaltoadmin_admin1.png)

10. Selecione **fornecedor de identidade** do painel de navegação esquerdo barra e clique em "Importar" para importar o ficheiro de metadados.

    ![Configurar da Palo Alto-início de sessão único](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_paloaltoadmin_admin2.png)

11. Execute os seguintes ações na janela de importação

    ![Configurar da Palo Alto-início de sessão único](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_paloaltoadmin_admin3.png)

    a. No **nome do perfil** caixa de texto, forneça por exemplo do nome da IU do administrador do Azure AD.
    
    b. No **metadados do fornecedor de identidade**, clique em **procurar** e selecione o ficheiro metadata.xml que transferiu a partir do portal do Azure
    
    c. Clique em **OK**

> [!TIP]
> Pode agora ler estas instruções dentro de uma versão concisa o [portal do Azure](https://portal.azure.com), enquanto estiver a configurar a aplicação!  Depois de adicionar esta aplicação a partir do **do Active Directory > aplicações da empresa** secção, basta clicar no **Single Sign-On** separador e aceder à documentação do embedded através de **configuração** secção na parte inferior. Pode ler mais sobre a funcionalidade de documentação incorporados aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD

O objetivo desta secção consiste em criar um utilizador de teste no portal do Azure chamado Britta Simon.

   ![Criar um utilizador de teste do Azure AD][100]

**Para criar um utilizador de teste no Azure AD, execute os seguintes passos:**

1. No portal do Azure, no painel esquerdo, clique em de **do Azure Active Directory** botão.

    ![O botão do Azure Active Directory](./media/active-directory-saas-paloaltoadmin-tutorial/create_aaduser_01.png)

2. Para apresentar a lista de utilizadores, aceda a **utilizadores e grupos**e, em seguida, clique em **todos os utilizadores**.

    !["Os utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-paloaltoadmin-tutorial/create_aaduser_02.png)

3. Para abrir o **utilizador** caixa de diálogo, clique em **adicionar** na parte superior do **todos os utilizadores** caixa de diálogo.

    ![O botão de adição](./media/active-directory-saas-paloaltoadmin-tutorial/create_aaduser_03.png)

4. No **utilizador** diálogo caixa, execute os seguintes passos:

    ![A caixa de diálogo de utilizador](./media/active-directory-saas-paloaltoadmin-tutorial/create_aaduser_04.png)

    a. No **nome** caixa, escreva **BrittaSimon**.

    b. No **nome de utilizador** caixa, escreva o endereço de e-mail do utilizador Britta Simon.

    c. Selecione o **mostrar palavra-passe** caixa de verificação e, em seguida, anote o valor que é apresentado no **palavra-passe** caixa.

    d. Clique em **Criar**.
 
### <a name="create-a-palo-alto-networks---admin-ui-test-user"></a>Criar um redes da Palo Alto - utilizador de teste de IU de Admin

Redes da Palo Alto - UI Admin suporta Just-in-time aprovisionamento de utilizadores para que um utilizador será automaticamente criado no sistema após a autenticação com êxito se este já não existe. Não precisa de efetuar qualquer ação aqui.

### <a name="assign-the-azure-ad-test-user"></a>Atribua o utilizador de teste do Azure AD

Nesta secção, vai ativar Britta Simon utilizar o Azure-início de sessão único, concedendo acesso às redes da Palo Alto - UI de Admin.

![Atribuir a função de utilizador][200] 

**Para atribuir Britta Simon a redes da Palo Alto - Admin IU, execute os seguintes passos:**

1. No portal do Azure, abra a vista de aplicações e, em seguida, navegue para a vista de diretório e aceda a **aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações, selecione **redes da Palo Alto - Admin IU**.

    ![As redes da Palo Alto - ligação de IU de administrador na lista de aplicações](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_paloaltoadmin_app.png)  

3. No menu à esquerda, clique em **utilizadores e grupos**.

    ![A ligação de "Utilizadores e grupos"][202]

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar atribuição][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista utilizadores.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão através do painel de acesso.

Ao clicar em redes da Palo Alto - mosaico de IU de administrador no painel de acesso, deve obter automaticamente com sessão iniciada para as redes da Palo Alto - a aplicação de IU de Admin.
Para mais informações sobre o painel de acesso, consulte [introdução ao painel de acesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicações SaaS com o Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_general_203.png

