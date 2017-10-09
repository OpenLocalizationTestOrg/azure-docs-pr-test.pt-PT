---
title: "Tutorial: Integração do Azure Active Directory com SAP HANA | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e SAP HANA."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 5ff6bfde0b1d7ab14025a4bc45199f9f826affd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a>Tutorial: Integração do Azure Active Directory com SAP HANA

Neste tutorial, saiba como toointegrate SAP HANA com o Azure Active Directory (Azure AD).

A integração de SAP HANA com o Azure AD fornece-lhe Olá seguintes vantagens:

- Pode controlar no Azure AD que tenha acesso tooSAP HANA
- Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooSAP HANA (Single Sign-On) com as respetivas contas do Azure AD
- Pode gerir as contas numa localização central - Olá portal do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos

integração do Azure AD com SAP HANA tooconfigure, terá de Olá seguintes itens:

- Uma subscrição do Azure AD
- Um SAP HANA-início de sessão único ativada subscrição
- Instância de um HANA em execução em qualquer IaaS público, no local, as VMs do Azure ou instâncias de grande SAP no Azure
- Olá XSA administração Web Interface, bem como Studio HANA instalada na instância do Olá HANA.

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção de SAP HANA. Teste integração Olá primeiro no desenvolvimento ou teste ambiente da aplicação Olá e, em seguida, ambiente de produção de Olá de utilização.

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

- Não utilize o seu ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste. cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:

1. A adição de SAP HANA de galeria Olá
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-sap-hana-from-hello-gallery"></a>A adição de SAP HANA de galeria Olá
tooconfigure Olá integração de SAP HANA com o Azure AD, é necessário tooadd SAP HANA Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd SAP HANA da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone. 

    ![botão de Azure Active Directory Olá][1]

2. Navegue demasiado**aplicações empresariais**. Em seguida, avance demasiado**todas as aplicações**.

    ![Painel de aplicações do Olá Enterprise][2]
    
3. tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.

    ![botão de aplicação nova Olá][3]

4. Na caixa de pesquisa de Olá, escreva **SAP HANA**, selecione **SAP HANA** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd. 

    ![Olá nova aplicação](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
Nesta secção, configure e teste do Azure AD-início de sessão único com SAP HANA com base num utilizador de teste chamado "Britta Simon."

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá SAP HANA é tooa utilizador no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá SAP HANA tem toobe estabelecida.

SAP HANA, atribuir valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.

tooconfigure e teste do Azure AD-início de sessão único com SAP HANA, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste de SAP HANA](#creating-a-sap-hana-test-user)**  -toohave um homólogo de Britta Simon no SAP HANA que é toohello ligado do Azure AD de representação do utilizador.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD-início de sessão único

Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação de SAP HANA.

**tooconfigure do Azure AD-início de sessão único com SAP HANA, execute Olá os seguintes passos:**

1. No Olá portal do Azure, no Olá **SAP HANA** página de integração de aplicações, clique em **de sessão único-**.

    ![Configurar o início de sessão único][4]

2. No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.
 
    ![Caixa de diálogo de início de sessão único](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. No Olá **SAP HANA domínio e os URLs** secção, execute Olá os seguintes passos:

    ![Domínio e os URLs únicos de informações de início de sessão](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    a. No Olá **identificador** caixa de texto, tipo como:`HA100` 

    b. No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`

    > [!NOTE] 
    > Estes valores não estiverem reais. Atualize estes valores com o URL de identificador e resposta real no Olá. Contacte [equipa de suporte de SAP HANA cliente](https://cloudplatform.sap.com/contact.html) tooget estes valores. 

4. No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.

    ![ligação de transferência do certificado Olá](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    >Se o certificado não está ativo, em seguida, torne-a ativa clicando Olá "disponibilizar novo certificado active" caixa de verificação no Olá do Azure AD. 

5. Aplicação de SAP HANA espera asserções de SAML Olá num formato específico. Olá seguinte captura de ecrã mostra um exemplo para este. Aqui iremos ter mapeado os Olá **identificador de utilizador** com **ExtractMailPrefix()** função do **user.mail**. Isto permite que o valor de prefixo Olá de e-mail do utilizador Olá que é Olá ID exclusivo do utilizador. Esta é enviada toohello aplicação de SAP HANA em cada resposta com êxito.

    ![Configurar o início de sessão único](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. No Olá **atributos de utilizador** secção em Olá **de sessão único-** diálogo:

    a. No Olá **identificador de utilizador** na lista pendente, selecione **ExtractMailPrefix**.
    
    b. No Olá **correio** na lista pendente, selecione **user.mail**.

7. Clique em **guardar** botão.

    ![Configurar botão único início de sessão guardar](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. tooconfigure-início de sessão único em **SAP HANA** lado, o início de sessão tooyour **HANA XSA Web consola** navegando toohello respetivo-ponto final de HTTPS.

    > [!Note]
    > Na configuração predefinida de Olá, Olá URL redireciona o ecrã início de sessão do Olá pedido tooa, que requer credenciais de Olá um autenticado SAP HANA da base de dados utilizador toocomplete Olá início de sessão do processo de. Olá utilizador inicia sessão tem de ter privilégios de Olá tooperform necessárias tarefas de administração de SAML.

9. Na Interface de Web XSA Olá, navegue demasiado**fornecedor de identidade** e a partir daí, clique em Olá **"+"** -botão no Olá parte inferior do painel do Olá ecrã toodisplay Olá adicionar informações do fornecedor de identidade e executar Olá os seguintes passos:

    ![Adicione o fornecedor de identidade](./media/active-directory-saas-saphana-tutorial/sap1.png)

    a. No Olá **adicionar informações do fornecedor de identidade** painel, colar Olá conteúdo Olá XML de metadados, que transferiu do portal do Azure para Olá **metadados** caixa de texto.

    ![Adicionar as definições do fornecedor de identidade](./media/active-directory-saas-saphana-tutorial/sap2.png)

    b. Se o conteúdo de Olá do documento XML Olá é válido, Olá análise processo extrai Olá tooinsert de informações necessárias para Olá **requerente, o ID de entidade e o emissor** campos no Olá geral dados ecrã área e Olá campos de URL no Olá Destino ecrã área, por exemplo,  **Base URL e o URL de SingleSignOn (*)**.

    ![Adicionar as definições do fornecedor de identidade](./media/active-directory-saas-saphana-tutorial/sap3.png)

    c. Na caixa de nome de Olá de Olá geral dados ecrã área, introduza um nome para o fornecedor de identidade de SAML SSO Olá novo.

    > [!Note]
    > nome de Olá de Olá SAML IDP é obrigatória e tem de ser exclusivo; -aparece na lista de Olá de IDPs SAML disponível que é apresentada se selecionar SAML como método de autenticação de Olá para SAP HANA XS toouse de aplicações, por exemplo, na área de ecrã de autenticação Olá da ferramenta de administração de artefacto XS Olá.

10. Guarde Olá os detalhes do Olá novo fornecedor de identidade. Escolha **guardar** toosave Olá detalhes do fornecedor de identidade Olá e adicione Olá novo SAML toohello lista de IDP de conhecidos IDPs de SAML.

    ![botão Guardar](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. No Studio HANA dentro das propriedades do sistema de Olá de Olá **configuração** separador, apenas filtrar definições por **saml** e ajustar Olá **assertion_timeout** de **10 seg** demasiado**seg 120**.

    ![definição de assertion_timeout](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!  Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá. Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.

![Criar utilizador do Azure AD][100]

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.

    ![botão de Azure Active Directory Olá](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.
    
    ![Olá "Utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.
 
    ![botão de adição de Olá](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. No Olá **utilizador** diálogo página, execute Olá os seguintes passos:
 
    ![caixa de diálogo utilizador Olá](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    a. No Olá **nome** caixa de texto, tipo **BrittaSimon**.

    b. No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.

    c. Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.

    d. Clique em **Criar**.
 
### <a name="creating-a-sap-hana-test-user"></a>Criar um utilizador de teste de SAP HANA

tooenable do Azure AD os utilizadores toolog no tooSAP HANA, estes têm de ser aprovisionados para SAP HANA.
SAP HANA suporta o aprovisionamento de just-in-time, que está por predefinição, ativada.

Se precisar de um utilizador de toocreate manualmente, execute Olá os seguintes passos:

>[!Note]
>Pode alterar autenticação externa Olá utilizada pelo utilizador Olá.
Os utilizadores externos são autenticados utilizando um sistema externo, por exemplo um sistema de Kerberos. Para obter informações detalhadas sobre as identidades externas, contacte o seu [administrador de domínio](https://cloudplatform.sap.com/contact.html).

1. Abra Olá [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) como administrador e ativar hello utilizador de base de dados para SAML SSO.

    ![Criar utilizador](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. Marcas de escala Olá caixa de verificação invisível toohello esquerda do **SAML** e siga Olá configurar ligação.

3. Clique em **adicionar** tooadd Olá SAML IDP e clique em **OK** selecionar Olá IDP de SAML adequado.

4. Adicionar Olá **identidade externas** (ex. BrittaSimon aqui) ou escolha **"Qualquer"** e clique em **OK**.

    >[!Note]
    >Se não estiver marcada "Qualquer" caixa de verificação, em seguida, tem de nome de utilizador de Olá no HANA tooexactly correspondência Olá nome de Olá utilizador no Olá UPN antes de sufixo de domínio Olá (ou seja, BrittaSimon@contoso.com iria ficar BrittaSimon no HANA).

5. Para fins de teste, atribuir todos os **"XS"** utilizador toohello de funções.

    ![atribuir funções](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > Deverá dar-essas permissões adequadas para os casos de utilização apenas.

6. Guarde o utilizador Olá.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD

Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooSAP HANA.

![Atribuir a função de utilizador Olá][200] 

**tooassign Britta Simon tooSAP HANA, execute Olá os seguintes passos:**

1. No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.

    ![Atribua o utilizador][201] 

2. Na lista de aplicações de Olá, selecione **SAP HANA**.

    ![Atribua o utilizador](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.

    ![ligação de "Utilizadores e grupos" Olá][202] 

4. Clique em **adicionar** botão. Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![Painel de atribuição de adicionar Olá][203]

5. No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.

6. Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.

7. Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste o início de sessão único

Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.

Ao clicar em mosaico de SAP HANA Olá no painel de acesso de Olá, deve obter a aplicação de SAP HANA tooyour automaticamente com sessão iniciada.
Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png

