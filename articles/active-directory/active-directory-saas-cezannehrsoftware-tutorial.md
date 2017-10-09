---
title: "Tutorial: Integração do Azure Active Directory com o software de RH Cezanne | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e o software de RH Cezanne."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 3675acd8871d62c2277def8074f7aa39ac46e2a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a>Tutorial: Integrar o Azure Active Directory com o software de RH Cezanne

Neste tutorial, saiba como toointegrate Cezanne HR software com o Azure Active Directory (Azure AD).

Integrar o software de RH Cezanne com o Azure AD fornece-lhe Olá seguintes vantagens. Pode:

- Controlar no Azure AD que tenha acesso tooCezanne HR software.
- Ative o seu início de sessão de tooautomatically utilizadores no software tooCezanne HR com início de sessão único (SSO) com as respetivas contas do Azure AD.
- Gerir as contas numa localização central: Olá portal do Azure.

toolearn mais informações sobre software como uma integração de aplicação de serviço (SaaS) com o Azure AD, consulte [que é o acesso a aplicações e SSO no Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com o software de RH Cezanne tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um software de RH Cezanne subscrição SSO ativado

> [!NOTE]
> tootest Olá obter os passos neste tutorial, recomendamos que utilize um ambiente de produção.

passos de Olá tootest neste tutorial, siga estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, testar o SSO do Azure AD num ambiente de teste. 

cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

* Adicionar software Cezanne HR da Galeria de Olá
* Configurar e testar o SSO do Azure AD

## <a name="add-cezanne-hr-software-from-hello-gallery"></a>Adicionar software Cezanne HR da Galeria de Olá
integração de Olá tooconfigure de RH Cezanne software com o Azure AD, adicione software Cezanne HR Olá Galeria tooyour na lista de aplicações SaaS geridas.

tooadd software Cezanne HR da Galeria de Olá, Olá seguintes:

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel esquerdo de Olá, selecione Olá **do Azure Active Directory** botão. 

    ![botão de "Do Azure Active Directory" Olá][1]

2. Selecione **aplicações empresariais** > **todas as aplicações**.

    ![Olá "Todas as aplicações" ligação][2]
    
3. tooadd uma nova aplicação, na parte superior de Olá de Olá **todas as aplicações** caixa de diálogo, selecione **nova aplicação**.

    ![Olá "Nova aplicação" botão][3]

4. Na caixa de pesquisa de Olá, escreva **Cezanne HR Software**.

    ![caixa de pesquisa de Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. Na lista de resultados de Olá, selecione **Cezanne HR Software** e, em seguida, selecione Olá **adicionar** botão a aplicação de Olá tooadd.

    ![lista de resultados de Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD-início de sessão único
Nesta secção, configurar e testar o SSO do Azure AD com o software de RH Cezanne com base num utilizador de teste chamado "Britta Simon."

Para SSO toowork, do Azure AD tem tooknow Olá Cezanne HR software homólogo toohello utilizador do Azure AD. Por outras palavras, tem de estabelecer uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá no Olá Cezanne HR software.

relação de ligação de Olá tooestablish, atribuir Olá Cezanne HR software **nome de utilizador** valor como Olá do Azure AD **Username** valor.

tooconfigure e teste do Azure AD SSO utilizando software de RH Cezanne, Olá concluir os seguintes blocos modulares.

### <a name="configure-azure-ad-sso"></a>Configurar o SSO do Azure AD

Nesta secção, pode ativar a SSO do Azure AD no portal do Azure de Olá e configurar o SSO na sua aplicação de software Cezanne HR, Olá seguinte:

1. No Olá portal do Azure, no Olá **Cezanne HR Software** página de integração de aplicações, selecione **de sessão único-**.

    ![Olá "De sessão único-" o comando][4]

2. tooenable SSO, no Olá **de sessão único-** caixa de diálogo, selecione de Olá **modo** como **baseados em SAML início de sessão**.
 
    ![caixa de "Modo de" Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. Em **Cezanne HR Software domínio e os URLs**, Olá a seguir:

    ![Olá "Cezanne HR Software domínio e os URLs" secção](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    a. No Olá **URL de início de sessão** caixa, escreva um URL que tem Olá a seguinte sintaxe:`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`

    b. No Olá **URL de resposta** caixa, escreva um URL que tem Olá a seguinte sintaxe:`https://w3.cezanneondemand.com:443/<tenantid>`    
     
    > [!NOTE] 
    > Olá anteriores valores não são reais. Atualize-as com o URL de resposta real Olá e o URL de início de sessão Olá. os valores de Olá tooobtain, Olá contacto [equipa de suporte de cliente de software Cezanne HR](mailto:info@cezannehr.com).

4. Em **certificado de assinatura de SAML**, selecione **certificado (Base64)**e, em seguida, guarde o ficheiro de certificado Olá no seu computador.

    ![Olá secção "Certificado de assinatura de SAML"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. Selecione **Guardar**.

    ![botão de "Guardar" Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. Em **Cezanne HR Software configuração**, selecione **configurar Cezanne HR Software** tooopen Olá **configurar início de sessão** janela. Olá cópia **ID de entidade de SAML** e **SAML único início de sessão no serviço** URL de Olá **referência rápida** secção.

    ![Olá secção "Configuração de Software de RH Cezanne"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. Numa janela do browser web diferente, inicie sessão no inquilino de software de RH Cezanne tooyour como administrador.

8. No painel esquerdo Olá, selecione **a configuração do sistema**. Selecione **definições de segurança** > **Single Sign-On configuração**.

    ![Olá "único início de sessão" a ligação de configuração](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. No Olá **permitir que os utilizadores toolog utilizando Olá os seguintes serviços único Sign-On (SSO)** painel, selecione de Olá **SAML 2.0** caixa de verificação e selecione Olá **configuração avançada** opção.

    ![O início de sessão único dos serviços de opções](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. Selecione **adicionar novos**.

    ![botão "Adicionar novo" Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. Em **fornecedores de identidade SAML 2.0**, Olá a seguir:

    ![Olá secção "Fornecedores de identidade SAML 2.0"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    a. No Olá **nome a apresentar** box, introduza o nome de Olá do seu fornecedor de identidade.

    b. No Olá **identificador da entidade** caixa, cole Olá **ID de entidade de SAML** que copiou do Olá portal do Azure. 

    c. No Olá **SAML enlace** caixa de lista, selecione **POST**.

    d. No Olá **ponto final de serviço de Token segurança** caixa, cole Olá **SAML único início de sessão no serviço** URL que copiou do Olá portal do Azure. 
    
    e. No Olá **nome de atributo de ID de utilizador** box, introduza `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
    
    f. Olá tooupload transferido o certificado do Azure AD, selecione de Olá **carregar** botão.
    
    g. Selecione **OK**. 

12. Selecione **Guardar**.

    ![botão de "Guardar" Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> Como configurar a aplicação Olá, pode ler uma versão de Olá precedente instruções no Olá concisa [portal do Azure](https://portal.azure.com). Depois de adicionar aplicação Olá de Olá **do Active Directory** > **aplicações empresariais** secção, selecione de Olá **de sessão único-** separador. Em seguida, Olá de acesso incorporados documentação de Olá **configuração** secção. 

toolearn mais informações sobre a funcionalidade de documentação incorporados Olá, consulte [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
Nesta secção, vai criar o utilizador de teste Britta Simon no Olá portal do Azure.

![utilizador de teste de Olá Britta Simon][100]

toocreate um utilizador de teste no Azure AD, Olá seguintes:

1. No Olá **portal do Azure**, no painel esquerdo de Olá, selecione Olá **do Azure Active Directory** botão.

    ![botão de "Do Azure Active Directory" Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, selecionadas **utilizadores e grupos** > **todos os utilizadores**.
    
    ![Olá "Todos os utilizadores" ligação](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    Olá **todos os utilizadores** é aberta a caixa de diálogo.

3. Olá tooopen **utilizador** caixa de diálogo, selecione **adicionar**.
 
    ![botão de "Adicionar" Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo caixa, Olá a seguir:
 
    ![caixa de diálogo Olá "Utilizador"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa, escreva **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa, escreva de utilizador Britta Simon **endereço de correio eletrónico**.

    c. Selecione Olá **mostrar palavra-passe** caixa de verificação e, em seguida, o valor de Olá de nota que foi gerado no Olá **palavra-passe** caixa.

    d. Selecione **Criar**.
 
### <a name="create-a-cezanne-hr-software-test-user"></a>Criar um utilizador de teste do software de RH Cezanne

tooenable do Azure AD os utilizadores toosign no software tooCezanne HR, estes têm de ser aprovisionados para Cezanne HR software. No caso de Olá de RH Cezanne software, o aprovisionamento é uma tarefa manual.

Aprovisionar uma conta de utilizador, Olá seguinte:

1.  Inicie sessão no tooyour Cezanne HR site da empresa de software como um administrador.

2.  No painel esquerdo Olá, selecione **a configuração do sistema** > **gerir utilizadores** > **adicionar novo utilizador**.

    ![ligação de "Adicionar novo utilizador" Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "novo utilizador")

3.  Em **pessoa detalhes**, Olá a seguir:

    ![Olá seção "Pessoa Detalhes"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "novo utilizador")
    
    a. Definir **utilizador interno** como **OFF**.
    
    b. No Olá **nome próprio** caixa, tipo Olá nome próprio do utilizador, por exemplo, **Britta**.  
 
    c. No Olá **Apelido** caixa, tipo Olá apelido do utilizador, por exemplo, **Simon**.
    
    d. No Olá **correio electrónico** caixa, escreva o endereço de e-mail do utilizador Olá, por exemplo, Brittasimon@contoso.com.

4.  Em **informações da conta**, Olá a seguir:

    ![Olá secção "Informações de conta"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "novo utilizador")
    
    a. No Olá **Username** caixa, escreva o endereço de e-mail do utilizador Olá, por exemplo, Brittasimon@contoso.com.
    
    b. No Olá **palavra-passe** caixa, escreva a palavra-passe do utilizador Olá.
    
    c. No Olá **função de segurança** caixa, selecione **HR Professional**.
    
    d. Selecione **OK**.

5. No Olá **de sessão único-** separador, Olá **SAML 2.0 identificadores** secção, selecione **adicionar novo**.

    ![botão "Adicionar novo" Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "utilizador")

6. No Olá **fornecedor de identidade** caixa de lista, selecione o seu fornecedor de identidade. No Olá **identificador de utilizador** box, introduza o endereço de correio eletrónico Olá para a conta de Simon de teste, utilizador Britta.

    ![Olá "Fornecedor de identidade" e "Utilizador identificador" caixas](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "utilizador")
    
7. Selecione **Guardar**.

    ![botão de "Guardar" Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "utilizador")

### <a name="assign-hello-azure-ad-test-user"></a>Atribua o utilizador de teste de Olá do Azure AD

Nesta secção, ativar o utilizador de teste Britta Simon toouse SSO do Azure, concedendo acesso tooCezanne HR software.

![Acesso de utilizador de teste][200] 

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, aceda a vista de diretório toohello. Selecione **aplicações empresariais** > **todas as aplicações**.

    ![Olá "Todas as aplicações" ligação][201] 

2. Na lista de aplicações de Olá, selecione **Cezanne HR Software**.

    ![lista de "Aplicações" Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. No menu de Olá Olá esquerda, selecione **utilizadores e grupos**.

    ![Atribua o utilizador][202] 

4. Selecione **Adicionar**. Em seguida, no Olá **adicionar atribuição** caixa de diálogo, selecione **utilizadores e grupos**.

    ![Ligação de "Utilizadores e grupos"][203]

5. No Olá **utilizadores e grupos** Olá caixa de diálogo **utilizadores** lista, selecione **Britta Simon**.

6. No Olá **utilizadores e grupos** caixa de diálogo, selecione **selecione**.

7. No Olá **adicionar atribuição** caixa de diálogo, selecione **atribuir**.
    
### <a name="test-sso"></a>Teste SSO

Nesta secção, testar a configuração do Azure AD SSO utilizando Olá painel de acesso.

Quando selecionar o mosaico de software Olá Cezanne HR no painel de acesso de Olá, inicie sessão no tooyour automaticamente a aplicação de software de RH Cezanne.

## <a name="next-steps"></a>Passos seguintes

* [Lista de tutoriais sobre como aplicações de SaaS toointegrate com o Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e SSO no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

