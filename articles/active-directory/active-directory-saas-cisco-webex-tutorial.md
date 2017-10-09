---
title: "Tutorial: Integração do Azure Active Directory com o Cisco Webex | Microsoft Docs"
description: "Saiba como toouse Cisco Webex com o Azure Active Directory tooenable único início de sessão, aprovisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9fc11e58a7acaa6fbfb32eeccbfbf85984950e67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a>Tutorial: Integração do Azure Active Directory com Cisco Webex
o objetivo deste tutorial Olá é integração de Olá tooshow do Azure e Cisco Webex.  
cenário de Olá descrito neste tutorial pressupõe que já tenha Olá seguintes itens:

* Uma subscrição do Azure válida
* Um inquilino Cisco Webex

Depois de concluir este tutorial, Olá utilizadores do Azure AD que atribuiu tooCisco Webex será toosingle capaz de início de sessão na aplicação Olá no site da sua empresa Cisco Webex (serviço fornecedor iniciada pelo início de sessão) ou utilizar Olá [toohello de introdução Aceder ao painel](active-directory-saas-access-panel-introduction.md).

cenário de Olá descrito neste tutorial consiste em Olá blocos modulares os seguintes:

* Ativar a integração de aplicações de Olá para Cisco Webex
* Configurar início de sessão único (SSO)
* Configurar o aprovisionamento de utilizadores
* Atribuir utilizadores

![Cenário](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "cenário")

## <a name="enable-hello-application-integration-for-cisco-webex"></a>Ativar a integração de aplicação Olá para Cisco Webex
o objetivo desta secção Olá é toooutline como integração de aplicações de Olá tooenable para Cisco Webex.

**integração de aplicações de Olá tooenable para Cisco Webex, execute Olá os seguintes passos:**

1. No Olá portal clássico do Azure, no painel de navegação esquerdo Olá, clique em **do Active Directory**.
   
   ![Do Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "do Active Directory")
2. De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.
3. Clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.
   
   ![Aplicações](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "aplicações")
4. Clique em **adicionar** em Olá parte inferior da página Olá.
   
   ![Adicionar aplicação](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Adicionar aplicação")
5. No Olá **que itens pretende toodo** caixa de diálogo, clique em **adicionar uma aplicação na Galeria de Olá**.
   
   ![Adicionar uma aplicação de gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "adicionar uma aplicação de gallerry")
6. No Olá **caixa pesquisa**, tipo **Cisco Webex**.
   
   ![Galeria de aplicações](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Galeria de aplicações")
7. No painel de resultados de Olá, selecione **Cisco Webex**e, em seguida, clique em **concluída** aplicação de Olá tooadd.
   
   ![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")
   
## <a name="configure-single-sign-on"></a>Configurar o início de sessão único

o objetivo desta secção Olá é toooutline como tooenable utilizadores tooauthenticate tooCisco Webex à respetiva conta no Azure AD com Federação com base no protocolo SAML Olá.  

Como parte deste procedimento, é necessário toocreate um certificado codificado base-64. Se não estiver familiarizado com este procedimento, consulte [como tooconvert um binário de certificado para um ficheiro de texto](http://youtu.be/PlgrzUZ-Y1o)

**tooconfigure único início de sessão, execute Olá os seguintes passos:**

1. No Olá portal clássico do Azure, no Olá **Cisco Webex** página de integração de aplicações, clique em **configurar o início de sessão único** tooopen Olá **configurar início de sessão único** caixa de diálogo.
   
   ![Configurar o início de sessão único](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "configurar o início de sessão único")
2. No Olá **como seria, como os utilizadores toosign no tooCisco Webex** página, selecione **Microsoft Azure AD Single Sign-On**e, em seguida, clique em **seguinte**.
   
   ![Configurar o início de sessão único](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "configurar o início de sessão único")
3. No Olá **URL da aplicação configurar** página, execute os seguintes passos de Olá e, em seguida, clique em **seguinte**.
   
   ![Configurar o URL da aplicação](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "configurar o URL da aplicação")   
   1. No Olá **iniciar sessão no URL** caixa de texto, escreva o URL de inquilino Cisco Webex (por ex.: *http://contoso.webex.com*).
   2. No Olá **URL de resposta do Cisco Webex** caixa de texto, tipo sua **Cisco Webex AssertionConsumerService URL** (por ex.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company* ).
4. No Olá **configurar o início de sessão único em Cisco Webex** página, toodownload o certificado, clique em **Transferir certificado**e, em seguida, guarde o ficheiro de certificado Olá no seu computador.
   
   ![Configurar o início de sessão único](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "configurar o início de sessão único")
5. Numa janela do browser web diferente, inicie sessão no site da sua empresa Cisco Webex como administrador.
6. No menu de Olá na parte superior do Olá, clique em **administração de sites**.
   
   ![Administração de sites](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "administração de sites")
7. No Olá **Gerir Site** secção, clique em **SSO configuração**.
   
   ![Configuração de SSO](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO configuração")
8. Na secção de configuração de SSO Web Federado Olá, efetue Olá os seguintes passos:
   
   ![Federado SSO configuração](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "federado SSO configuração")  
   1. De Olá **protocolo Federation** lista, selecione **SAML 2.0**.
   2. Criar um **com codificação Base 64** ficheiro a partir do seu certificado transferido.  
    >[!TIP]
    >Para obter mais detalhes, consulte [como tooconvert um binário de certificado para um ficheiro de texto](http://youtu.be/PlgrzUZ-Y1o)
    >  
   3. Abra o certificado codificado base-64 no bloco de notas e, em seguida, Olá copiar conteúdo do mesmo.
   4. Clique em **importar metadados de SAML**e, em seguida, cole o certificado codificado base-64.
   5. No Olá portal clássico do Azure, no Olá **configurar o início de sessão único em Cisco Webex** página da caixa de diálogo, Olá cópia **URL do emissor** valor e, em seguida, cole-o Olá **emissor para SAML (IdP ID)** caixa de texto.
   6. No Olá portal clássico do Azure, no Olá **configurar o início de sessão único em Cisco Webex** página da caixa de diálogo, Olá cópia **URL de início de sessão remoto** valor e, em seguida, cole-o Olá **o início de sessão do cliente SSO serviço URL** caixa de texto.
   7. De Olá **NameID formato** lista, selecione **endereço de correio eletrónico**.
   8. No Olá **AuthnContextClassRef** caixa de texto, tipo **urn: oasis: os nomes: tc: SAML:2.0:ac:classes:Password**.
   9. No Olá portal clássico do Azure, no Olá **configurar o início de sessão único em Cisco Webex** página da caixa de diálogo, Olá cópia **URL de fim de sessão remoto** valor e, em seguida, cole-o Olá **fim de sessão do cliente SSO serviço URL** caixa de texto.
   10. Clique em **atualização**.
9. No Olá portal clássico do Azure, no Olá **configurar o início de sessão único em Cisco Webex** página da caixa de diálogo, selecione a confirmação de configuração de início de sessão único Olá e, em seguida, clique em **concluída**.
   
   ![Configurar o início de sessão único](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "configurar o início de sessão único")
   
## <a name="configure-user-provisioning"></a>Configurar o aprovisionamento de utilizadores

Na ordem tooenable do Azure AD os utilizadores toolog para Cisco Webex, têm de ser aprovisionados para Cisco Webex.  

* No caso de Olá da Cisco Webex, o aprovisionamento é uma tarefa manual.

**executar de contas de utilizador, tooprovision Olá os seguintes passos:**

1. Inicie sessão no tooyour **Cisco Webex** inquilino.
2. Aceda demasiado**gerir utilizadores \> adicionar utilizador**.
   
   ![Adicionar utilizadores](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "adicionar utilizadores")
3. Na secção de adicionar utilizador Olá, execute Olá os seguintes passos:
   
   ![Adicionar utilizador](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "adicionar utilizador")   
   1. Como **tipo de conta**, selecione **anfitrião**.
   2. Escreva as informações de Olá de um utilizador do Azure AD existente no Olá seguintes caixas de texto: **nome próprio, apelido**, **nome de utilizador**, **E-Mail**, **depalavra-passe**, **Confirmar palavra-passe**.
   3. Clique em **Adicionar**.

>[!NOTE]
>Pode utilizar quaisquer outras Cisco Webex utilizador conta criação ferramentas ou APIs fornecidas pelo Cisco Webex tooprovision contas de utilizador do AAD. 
> 

## <a name="assign-users"></a>Atribuir utilizadores
tootest a configuração, terá de toogrant Olá do Azure AD utilizadores tooallow utilizando o tooit de acesso de aplicação atribuindo-los.

**tooassign utilizadores tooCisco Webex, execute Olá os seguintes passos:**

1. Olá portal clássico do Azure, crie uma conta de teste.
2. No Olá **Cisco Webex** página de integração de aplicações, clique em **atribuir utilizadores**.
   
   ![Atribuir utilizadores](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "atribuir utilizadores")
3. Selecione o utilizador de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm a atribuição.
   
   ![Sim](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Sim")

Se quiser tootest as definições de início de sessão único, abra Olá painel de acesso. Para obter mais detalhes sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).

