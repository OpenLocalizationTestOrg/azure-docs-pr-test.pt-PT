---
title: "Tutorial: Integração do Azure Active Directory a área de trabalho por Facebook | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e à área de trabalho por Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f71a59527394730757d501a973251dc293fd3683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a>Tutorial: Integração do Azure Active Directory a área de trabalho por Facebook

Neste tutorial, saiba como toointegrate à área de trabalho por Facebook no Azure Active Directory (Azure AD).

Área de trabalho por Facebook a integração com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooWorkplace por Facebook
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooWorkplace por Facebook (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD a área de trabalho por Facebook tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Uma área de trabalho por Facebook-início de sessão único ativada subscrição

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. Adicionar à área de trabalho por Facebook da Galeria de Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-workplace-by-facebook-from-hello-gallery"></a>Adicionar à área de trabalho por Facebook da Galeria de Olá
tooconfigure Olá integração da área de trabalho por Facebook com o Azure AD, é necessário tooadd à área de trabalho por Facebook Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd à área de trabalho por Facebook da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![Active Directory][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Aplicações][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![Aplicações][3]

4. Na caixa de pesquisa de Olá, escreva **à área de trabalho por Facebook**.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. No painel de resultados de Olá, selecione **à área de trabalho por Facebook**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configurar e testar o Azure AD-início de sessão único a área de trabalho por Facebook com base num utilizador de teste chamado "Britta Simon."

Para único início de sessão toowork, do Azure AD tem tooknow qual o utilizador que homólogo Olá na área de trabalho por Facebook é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá na área de trabalho por Facebook tem toobe estabelecida.

Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** na área de trabalho por Facebook.

tooconfigure e teste do Azure AD-início de sessão único, a área de trabalho, Facebook, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Configurar a frequência de reautenticação](#configuring-reauthentication-frequency)**  -tooconfigure tooprompt de área de trabalho para uma verificação SAML.
3. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
4. **[Criar uma área de trabalho por utilizador de teste do Facebook](#creating-a-workplace-by-facebook-test-user)**  -toohave um homólogo de Britta Simon na área de trabalho por Facebook é toohello ligado do Azure AD de representação do utilizador.
5. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
6. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, ativar o Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua área de trabalho por aplicação do Facebook.

**tooconfigure do Azure AD-início de sessão único a área de trabalho, Facebook, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **à área de trabalho por Facebook** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Configurar o início de sessão único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. No Olá **à área de trabalho ao domínio do Facebook e URLs** secção, execute Olá os seguintes passos:

    ![Configurar o início de sessão único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    a. No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<instancename>.facebook.com`

    b. No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://www.facebook.com/company/<instancename>`

    > [!NOTE] 
    > Estes valores não estiverem Olá real. Atualizar estes valores com Olá real URL de início de sessão e o identificador. Contacte [à área de trabalho pela equipa de suporte de cliente do Facebook](https://workplace.fb.com/faq/) tooget estes valores. 

4. No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![Configurar o início de sessão único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. Clique em **guardar** botão.

    ![Configurar o início de sessão único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. No Olá **à área de trabalho pela configuração do Facebook** secção, clique em **configurar área de trabalho por Facebook** tooopen **configurar início de sessão** janela. Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**

    ![Configurar o início de sessão único](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. Numa janela do browser web diferente, tooyour de início de sessão à área de trabalho por site de empresa do Facebook como administrador.
  
   > [!NOTE] 
   > Como parte do Olá processo de autenticação SAML, à área de trabalho pode utilizar cadeias de consulta de cópia de segurança too2.5 quilobytes em tamanho em ordem toopass parâmetros tooAzure AD.

8. No Olá **Dashboard da empresa**, aceda a toohello **autenticação** separador.

9. Em **autenticação SAML**, selecione **SSO apenas** de Olá na lista pendente.

10. Os valores de entrada Olá copiados **à área de trabalho pela configuração do Facebook** secção Olá portal do Azure em campos correspondente Olá:

    *   No **SAML URL** caixa de texto, colar Olá valor **URL Single Sign-On serviço**, que copiou do portal do Azure.
    *   No **caixa de texto do URL do emissor de SAML**, cole o valor de Olá de **ID de entidade de SAML**, que copiou do portal do Azure.
    *   No **redirecionamento de fim de sessão SAML** (opcional), cole o valor Olá **Sign-Out URL**, que copiou do portal do Azure.
    *   Abra o **certificado com codificação base 64** no bloco de notas transferido a partir do portal do Azure, copiar o conteúdo de Olá-lo na sua área de transferência e, em seguida, cole-toothe **SAML certificado** caixa de texto.

11. Poderá ser necessário tooenter Olá URL público-alvo, URL de destinatário, e o URL de ACS (serviço de consumidor asserção) listados em Olá **configuração SAML** secção.

12. Desloque-se na parte inferior de toohello da secção de Olá e clique em Olá **teste SSO** botão. Isto resulta numa janela de pop-up apresentação com a página de início de sessão do Azure AD apresentados. Introduza as suas credenciais como normal tooauthenticate. 

    **Resolução de problemas:** endereço de correio eletrónico Olá Certifique-se de que está a ser devolvido atrás do Azure AD é Olá igual ao hello conta à área de trabalho, o qual iniciou sessão com.

13. Depois de teste de Olá foi concluída com êxito, desloque-se toohello inferior da página Olá e clique em Olá **guardar** botão.

14. Todos os utilizadores usem à área de trabalho serão agora apresentados com a página de início de sessão do Azure AD para autenticação.

15. **Redirecionamento de fim de sessão de SAML (opcional)** - 

    Pode escolher toooptionally configurar um Url de fim de sessão SAML, que pode ser utilizado toopoint na página de fim de sessão do Azure AD. Quando esta definição está ativada e configurada, o utilizador Olá deixará de estar página de fim de sessão do toohello direcionados à área de trabalho. Em vez disso, o utilizador Olá será redirecionada toohello url que foi adicionado na definição de redirecionamento de fim de sessão SAML Olá.


> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="configuring-reauthentication-frequency"></a>Configurar a frequência de reautenticação rápida

Pode configurar tooprompt à área de trabalho para uma verificação SAML diariamente, três dias, semanas, duas semanas, meses ou nunca.

> [!NOTE] 
>Olá valor mínimo para a verificação SAML Olá em aplicações móveis está definido tooone semana.

Pode também forçar um SAML repor para todos os utilizadores com o botão de Olá: exigir autenticação SAML para todos os utilizadores agora.


### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-workplace-by-facebook-test-user"></a>Criar uma área de trabalho por utilizador de teste do Facebook

Nesta secção, um utilizador chamado Britta Simon é criado na área de trabalho por Facebook. Área de trabalho por Facebook suporta o aprovisionamento de just-in-time, que está ativada por predefinição.

Não há nenhuma ação por si nesta secção. Se um utilizador não existe na área de trabalho, Facebook, uma nova é criada quando tenta tooaccess à área de trabalho por Facebook.

>[!Note]
>Se precisar de toocreate manualmente, contacte um utilizador [à área de trabalho pela equipa de suporte de cliente do Facebook](https://workplace.fb.com/faq/)

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooWorkplace por Facebook.

![Atribua o utilizador][200] 

**tooassign Britta Simon tooWorkplace por Facebook, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **à área de trabalho por Facebook**.

    ![Configurar o início de sessão único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Atribua o utilizador][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Se quiser tootest as definições de início de sessão único, abra Olá painel de acesso.
Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar o aprovisionamento de utilizadores](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

