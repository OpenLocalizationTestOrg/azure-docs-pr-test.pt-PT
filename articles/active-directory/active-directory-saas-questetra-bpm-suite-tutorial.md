---
title: "Tutorial: Integração do Azure Active Directory com Questetra BPM Suite | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Questetra BPM Suite."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 4907e3b5751cd79f994fbd2ebcb7faec4eac34e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a>Tutorial: Integração do Azure Active Directory com Questetra BPM Suite
o objetivo deste tutorial Olá é tooshow como toointegrate Questetra BPM Suite com o Azure Active Directory (Azure AD).  
Integrar Questetra BPM Suite com o Azure AD fornece-lhe Olá seguintes vantagens: 

* Pode controlar no Azure AD que tenha acesso tooQuestetra BPM Suite 
* Pode ativar a utilizadores tooautomatically get com sessão iniciada tooQuestetra Suite BPM (Single Sign-On) com as respetivas contas do Azure AD
* Pode gerir as contas numa localização central - Olá portal clássico do Azure

Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Pré-requisitos
integração do Azure AD com Questetra BPM Suite tooconfigure, terá de Olá seguintes itens:

* Uma subscrição do Azure AD
* Um [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) início de sessão único subscrição ativado

> [!NOTE]
> Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.
> 
> 

tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:

* Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.
* Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Descrição do cenário
o objetivo deste tutorial Olá é tooenable tootest do Azure AD-início de sessão único num ambiente de teste.  
cenário de Olá descrito neste tutorial consiste em três blocos modulares principais:

1. Adicionar Questetra BPM Suite da Galeria de Olá 
2. Configurar e testar o Azure AD de sessão único-

## <a name="adding-questetra-bpm-suite-from-hello-gallery"></a>Adicionar Questetra BPM Suite da Galeria de Olá
tooconfigure Olá integração do Questetra BPM Suite com o Azure AD, é necessário tooadd Questetra BPM Suite Olá Galeria tooyour na lista de aplicações SaaS geridas.

**tooadd Questetra BPM Suite da Galeria de Olá, execute Olá os seguintes passos:**

1. No Olá **portal clássico do Azure**, no painel de navegação esquerdo de Olá, clique em **do Active Directory**. 
   
    ![Active Directory][1]

2. De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.

3. Clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.
   
    ![Aplicações][2]

4. Clique em **adicionar** em Olá parte inferior da página Olá.
   
    ![Aplicações][3]

5. No Olá **que itens pretende toodo** caixa de diálogo, clique em **adicionar uma aplicação na Galeria de Olá**.
   
    ![Aplicações][4]

6. Na caixa de pesquisa de Olá, escreva **Questetra BPM Suite**.
   
    ![Aplicações][5]

7. No painel de resultados de Olá, selecione **Questetra BPM Suite**e, em seguida, clique em **concluída** aplicação de Olá tooadd.

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD de sessão único-
o objetivo desta secção Olá é tooshow que como tooconfigure e teste do Azure AD-início de sessão único com Questetra BPM Suite com base num utilizador de teste chamado "Britta Simon".

Para único início de sessão toowork, do Azure AD tem tooknow que utilizador do homólogo Olá utilizador de tooan Questetra BPM Suite no Azure AD. Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Questetra BPM Suite tem toobe estabelecida.  
Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no Questetra BPM Suite.

tooconfigure e teste do Azure AD-início de sessão único com Questetra BPM Suite, terá de Olá toocomplete blocos modulares os seguintes:

1. **[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.
2. **[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.
3. **[Criar um utilizador de teste Questetra BPM Suite](#creating-a-questetra-bpm-suite-test-user)**  -toohave um homólogo de Britta Simon no Questetra BPM Suite que é a representação de toohello ligado do Azure AD de forma.
4. **[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.
5. **[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurar o Azure AD início de sessão único
o objetivo desta secção Olá é tooenable do Azure AD início de sessão no portal clássico do Azure de Olá e tooconfigure-início de sessão único na sua aplicação Questetra BPM Suite.

**tooconfigure do Azure AD-início de sessão único com Questetra BPM Suite, execute Olá os seguintes passos:**

1. No Olá portal clássico do Azure, no Olá **Questetra BPM Suite** página de integração de aplicações, clique em **configurar o início de sessão único** tooopen Olá **configurar Single Sign-On**  caixa de diálogo.
   
    ![Configurar o início de sessão único][8]

2. No Olá **como seria, como os utilizadores toosign no tooQuestetra BPM Suite** página, selecione **do Azure AD Single Sign-On**e, em seguida, clique em **seguinte**.
   
    ![Azure AD início de sessão único][9]

3. Numa janela do browser web diferente, inicie sessão no seu **Questetra BPM Suite** site da empresa como administrador.

4. No menu de Olá na parte superior do Olá, clique em **definições do sistema**. 
   
    ![Azure AD início de sessão único][10]

5. Olá tooopen **SingleSignOnSAML** página, clique em **SSO (SAML)**. 
   
    ![Azure AD início de sessão único][11]

6. No Olá portal clássico do Azure, no Olá **configurar definições de aplicação** diálogo página, execute Olá os seguintes passos: 
   
    ![Configurar definições da aplicação][13]
   
    a. No **Questetra BPM Suite** site da empresa, no Olá secção de informações de SP, Olá cópia **ACS URL**e, em seguida, cole-o Olá **URL de início de sessão** caixa de texto.
   
    b. No **Questetra BPM Suite** site da empresa, no Olá secção de informações de SP, Olá cópia **ID de entidade**e, em seguida, cole-o Olá **URL do emissor** caixa de texto.
   
    c. No **Questetra BPM Suite** site da empresa, no Olá secção de informações de SP, Olá cópia **ACS URL**e, em seguida, cole-o Olá **URL de resposta** caixa de texto.
   
    d. Clique em **Seguinte**.

7. No Olá **configurar o início de sessão único em Questetra BPM Suite** página, clique em **Transferir certificado**e, em seguida, guarde o ficheiro de certificado Olá localmente no seu computador.
   
    ![Configurar o início de sessão único][14]

8. No **Questetra BPM Suite** da empresa site, execute Olá os seguintes passos: 
   
    ![Configurar o início de sessão único][15]
   
    a. Selecione **ativar o início de sessão único**.
   
    b. No portal clássico do Azure Olá, copie Olá **URL do emissor** valor e, em seguida, cole-o Olá **ID de entidade** caixa de texto.
   
    c. No portal clássico do Azure Olá, copie Olá **URL Single Sign-On serviço** valor e, em seguida, cole-o Olá **URL de página de início de sessão** caixa de texto.
   
    d. No portal clássico do Azure Olá, copie Olá **único URL de serviço Sign-Out** valor e, em seguida, cole-o Olá **URL da página de início de sessão** caixa de texto.
   
    e. No Olá **NameID formato** caixa de texto, tipo **urn: oasis: os nomes: tc: SAML:1.1:nameid-formato: endereço de correio eletrónico**.

    f. Crie um ficheiro codificado base-64 do seu certificado transferido. 

    >[!TIP] 
    >Para obter mais detalhes, consulte [como tooconvert um binário de certificado para um ficheiro de texto](http://youtu.be/PlgrzUZ-Y1o).

    g. Abra o certificado codificado base-64 no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência e, em seguida, cole-o Olá **certificado validação** caixa de texto. 

    h. Clique em **Guardar**.

1. No portal clássico do Azure Olá, selecione a confirmação de configuração de início de sessão único Olá e, em seguida, clique em **seguinte**. 
   
    ![O que é o Azure AD Connect][17]

2. No Olá **único início de sessão confirmação** página, clique em **concluída**.  
   
    ![O que é o Azure AD Connect][18]


### <a name="creating-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD
o objetivo desta secção Olá é toocreate um utilizador de teste no portal clássico do Azure chamado Britta Simon de Olá.

**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**

1. No Olá **portal clássico do Azure**, no painel de navegação esquerdo de Olá, clique em **do Active Directory**.
   
    ![Criar utilizador de teste do Azure AD][100] 

2. De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.

3. lista de Olá toodisplay de utilizadores, no menu de Olá na parte superior do Olá, clique em **utilizadores**.
   
    ![Criar utilizador de teste do Azure AD][101] 

4. Olá tooopen **adicionar utilizador** caixa de diálogo, na barra de ferramentas de Olá na parte inferior do Olá, clique em **adicionar utilizador**. 
   
    ![Criar utilizador de teste do Azure AD][102] 

5. No Olá **diga-nos informações sobre este utilizador** diálogo página, execute Olá os seguintes passos:
   
    ![Criar utilizador de teste do Azure AD][103]
   
    a. Como **tipo de utilizador**, selecione **novo utilizador na sua organização**.
   
    b. No nome de utilizador de Olá **textbox**, tipo **BrittaSimon**.
   
    c. Clique em Seguinte.

6. No Olá **perfil de utilizador** diálogo página, execute Olá os seguintes passos: 
   
    ![Criar utilizador de teste do Azure AD][104] 
   
    a. No Olá **nome próprio** caixa de texto, tipo **Britta**. 
   
    b. No Olá **Apelido** caixa de texto, tipo, **Simon**.
   
    c. No Olá **nome a apresentar** caixa de texto, tipo **Britta Simon**.
   
    d. No Olá **função** lista, selecione **utilizador**.
   
    e. Clique em **Seguinte**.

7. No Olá **Get palavra-passe temporária** página da caixa de diálogo, clique em **criar**.
   
    ![Criar utilizador de teste do Azure AD][105]  

8. No Olá **Get palavra-passe temporária** diálogo página, execute Olá os seguintes passos:
   
    ![Criar utilizador de teste do Azure AD][106]   
   
    a. Anote o valor Olá Olá **nova palavra-passe**.
   
    b. Clique em **Concluído**.   

### <a name="creating-a-questetra-bpm-suite-test-user"></a>Criar um utilizador de teste Questetra BPM Suite
o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon no Questetra BPM Suite.

**toocreate um utilizador chamar Britta Simon Questetra BPM Suite, execute Olá os seguintes passos:**

1. Início de sessão tooyour Questetra BPM Suite site da empresa como administrador.
2. Aceda demasiado**definições do sistema > lista de utilizadores > novo utilizador**. 
3. Na caixa de diálogo de novo utilizador Olá, execute Olá os seguintes passos: 
   
    ![Criar utilizador de teste][300] 
   
    a. No Olá **nome** caixa de texto, escreva o nome de utilizador de Britta no Azure AD.
   
    b. No Olá **E-Mail** caixa de texto, escreva o nome de utilizador de Britta no Azure AD.
   
    c. No Olá **palavra-passe** caixa de texto, escreva um palavra-passe.

4. Clique em **adicionar novo utilizador**.

### <a name="assigning-hello-azure-ad-test-user"></a>Atribuir o utilizador de teste de Olá do Azure AD
o objetivo desta secção Olá é tooenabling Britta Simon toouse do Azure-início de sessão único, concedendo tooQuestetra respetivo acesso BPM Suite.

![O que é o Azure AD Connect][200]

**tooassign Britta Simon tooQuestetra BPM Suite, execute Olá os seguintes passos:**

1. Olá, Azure portal clássico, a vista de aplicações Olá tooopen, na vista de diretório Olá, clique em **aplicações** no menu superior Olá.
   
    ![O que é o Azure AD Connect][201]
2. Na lista de aplicações de Olá, selecione **Questetra BPM Suite**.
   
    ![O que é o Azure AD Connect][205]
3. No menu de Olá na parte superior do Olá, clique em **utilizadores**.
   
    ![O que é o Azure AD Connect][202]
4. Na lista de utilizadores Olá, selecione **Britta Simon**.
   
    ![O que é o Azure AD Connect][203]
5. Na barra de ferramentas Olá na parte inferior de Olá, clique em **atribuir**.
   
    ![O que é o Azure AD Connect][204]

### <a name="testing-single-sign-on"></a>Teste o início de sessão único
o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.  
Ao clicar em mosaico de Questetra BPM Suite Olá no painel de acesso de Olá, deve obter a aplicação de Questetra BPM Suite tooyour automaticamente com sessão iniciada.

## <a name="additional-resources"></a>Recursos Adicionais
* [Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
