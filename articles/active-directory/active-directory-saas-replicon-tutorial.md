---
title: "Tutorial: Integração do Azure Active Directory com Replicon | Microsoft Docs"
description: "Saiba como toouse Replicon com o Azure Active Directory tooenable único início de sessão, aprovisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 4949eaf959265cfa4f732a2b73317fffe6312a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a>Tutorial: Integração do Azure Active Directory com Replicon
o objetivo deste tutorial Olá é integração de Olá tooshow do Azure e Replicon. cenário de Olá descrito neste tutorial pressupõe que já tenha Olá seguintes itens:

* Uma subscrição do Azure válida
* Um inquilino Replicon

Depois de concluir este tutorial, os utilizadores Olá do Azure AD que atribuiu tooReplicon será toosingle capazes sessão numa aplicação Olá no site da sua empresa Replicon (serviço fornecedor iniciada pelo início de sessão) ou utilizar Olá [introdução toohello acesso Painel](active-directory-saas-access-panel-introduction.md).

cenário de Olá descrito neste tutorial consiste em Olá blocos modulares os seguintes:

1. Ativar a integração de aplicações de Olá para Replicon
2. Configurar início de sessão único (SSO)
3. Configurar o aprovisionamento de utilizadores
4. Atribuir utilizadores

![Cenário](./media/active-directory-saas-replicon-tutorial/IC777798.png "cenário")

## <a name="enable-hello-application-integration-for-replicon"></a>Ativar a integração de aplicação Olá para Replicon
o objetivo desta secção Olá é toooutline como integração de aplicações de Olá tooenable para Replicon.

**integração de aplicações de Olá tooenable para Replicon, execute Olá os seguintes passos:**

1. No Olá portal clássico do Azure, no painel de navegação esquerdo Olá, clique em **do Active Directory**.
   
    ![Do Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "do Active Directory")
2. De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.
3. Clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.
   
    ![Aplicações](./media/active-directory-saas-replicon-tutorial/IC700994.png "aplicações")
4. Clique em **adicionar** em Olá parte inferior da página Olá.
   
    ![Adicionar aplicação](./media/active-directory-saas-replicon-tutorial/IC749321.png "Adicionar aplicação")
5. No Olá **que itens pretende toodo** caixa de diálogo, clique em **adicionar uma aplicação na Galeria de Olá**.
   
    ![Adicionar uma aplicação de gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "adicionar uma aplicação de gallerry")
6. No Olá **caixa pesquisa**, tipo **Replicon**.
   
    ![Galeria de aplicações](./media/active-directory-saas-replicon-tutorial/IC777799.png "Galeria de aplicações")
7. No painel de resultados de Olá, selecione **Replicon**e, em seguida, clique em **concluída** aplicação de Olá tooadd.
   
    ![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")
   
## <a name="configure-single-sign-on"></a>Configurar o início de sessão único

o objetivo desta secção Olá é toooutline como tooenable utilizadores tooauthenticate tooReplicon à respetiva conta no Azure AD com Federação com base no protocolo SAML Olá.

**tooconfigure único início de sessão, execute Olá os seguintes passos:**

1. No Olá portal clássico do Azure, no Olá **Replicon** página de integração de aplicações, clique em **configurar o início de sessão único** tooopen Olá **configurar início de sessão único** caixa de diálogo.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-replicon-tutorial/IC777801.png "configurar o início de sessão único")
2. No Olá **como seria, como os utilizadores toosign no tooReplicon** página, selecione **Microsoft Azure AD Single Sign-On**e, em seguida, clique em **seguinte**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-replicon-tutorial/IC777802.png "configurar o início de sessão único")
3. No Olá **URL da aplicação configurar** página, execute Olá os seguintes passos:
   
    ![Configurar o URL da aplicação](./media/active-directory-saas-replicon-tutorial/IC777803.png "configurar o URL da aplicação")
  1. No Olá **Replicon no URL sessão** caixa de texto, escreva o URL de inquilino Replicon (por ex.: *https://na2.replicon.com/company/saml2/sp-sso/post*).
  2. No Olá **URL de resposta de Replicon** caixa de texto, escreva o seu Replicon **AssertionConsumerService** URL (por ex.: *https://global.replicon.com/! / saml2/empresa/sso/post*).  
      
     >[!NOTE]
     >Pode obter Olá URL de metadados de Replicon Olá em: **https://global.replicon.com/! /saml2/\<YourCompanyKey\>**.
     > 
     > 
 
  3. Clique em **Seguinte**.

4. No Olá **configurar o início de sessão único em Replicon** página, toodownload os seus metadados, clique em **transferir metadados**e, em seguida, guarde Olá metadados no seu computador.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-replicon-tutorial/IC777804.png "configurar o início de sessão único")
5. Numa janela do browser web diferente, inicie sessão no site da sua empresa Replicon como administrador.

6. tooconfigure SAML 2.0, execute Olá os seguintes passos:
   
    ![Ativar a autenticação SAML](./media/active-directory-saas-replicon-tutorial/IC777805.png "autenticação ativar SAML")
  
  1. Olá toodisplay **EnableSAML Authentication2** caixa de diálogo, acrescentar Olá os seguintes tooyour URL, após a sua chave de empresa: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**  
    * seguinte Olá mostra esquema Olá do URL de conclusão de Olá:  
   **https://Na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**
   2. Clique em Olá  **+**  tooexpand Olá **v20Configuration** secção.
   3. Clique em Olá  **+**  tooexpand Olá **metaDataConfiguration** secção.
   4. Clique em **Escolher ficheiro**, tooselect o ficheiro de XML de metadados de fornecedor de identidade e clique em **submeter**.

7. No portal clássico do Azure Olá, selecione a confirmação de configuração de início de sessão único Olá e, em seguida, clique em **concluída** tooclose Olá **configurar início de sessão único** caixa de diálogo.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-replicon-tutorial/IC778418.png "configurar o início de sessão único")
   
## <a name="configure-user-provisioning"></a>Configurar o aprovisionamento de utilizadores

Na ordem tooenable do Azure AD os utilizadores toolog para Replicon, têm de ser aprovisionados para Replicon.  

No caso de Olá da Replicon, o aprovisionamento é uma tarefa manual.

**tooconfigure aprovisionamento de utilizadores, execute Olá os seguintes passos:**

1. Numa janela do browser web, inicie sessão no site da sua empresa Replicon como administrador.
2. Aceda demasiado**administração \> utilizadores**.
   
    ![Os utilizadores](./media/active-directory-saas-replicon-tutorial/IC777806.png "utilizadores")
3. Clique em **+ adicionar utilizador**.
   
    ![Adicionar utilizador](./media/active-directory-saas-replicon-tutorial/IC777807.png "adicionar utilizador")
4. No Olá **perfil de utilizador** secção, execute Olá os seguintes passos:
   
    ![Perfil de utilizador](./media/active-directory-saas-replicon-tutorial/IC777808.png "perfil de utilizador")
   
  1. No Olá **nome de início de sessão** caixa de texto, Olá de tipo do Azure AD endereço de e-mail do utilizador Olá do Azure AD que pretende tooprovision.
  2. Como **tipo de autenticação**, selecione **SSO**.
  3. No Olá **departamento** caixa de texto, escreva o departamento de utilizador Olá.
  4. Como **empregado tipo**, selecione **administrador**.
  5. Clique em **guardar o perfil de utilizador**.

>[!NOTE]
>Pode utilizar quaisquer outras Replicon utilizador conta criação ferramentas ou APIs fornecidas pelo Replicon tooprovision contas de utilizador do AAD.
> 
> 

## <a name="assign-users"></a>Atribuir utilizadores
tootest a configuração, terá de toogrant Olá do Azure AD utilizadores tooallow utilizando o tooit de acesso de aplicação atribuindo-los.

**tooassign tooReplicon de utilizadores, efetuar Olá os seguintes passos:**

1. Olá portal clássico do Azure, crie uma conta de teste.

2. No Olá **Replicon** página de integração de aplicações, clique em **atribuir utilizadores**.
   
    ![Atribuir utilizadores](./media/active-directory-saas-replicon-tutorial/IC777809.png "atribuir utilizadores")

3. Selecione o utilizador de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm a atribuição.
   
    ![Sim](./media/active-directory-saas-replicon-tutorial/IC767830.png "Sim")

Se quiser tootest as definições de início de sessão único, abra Olá painel de acesso. Para obter mais detalhes sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).

