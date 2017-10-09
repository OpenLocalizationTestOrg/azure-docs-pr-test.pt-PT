---
title: "Tutorial: Integração do Azure Active Directory com o ciclo de vida SCC | Microsoft Docs"
description: "Saiba como toouse SCC ciclo de vida com o Azure Active Directory tooenable único início de sessão, aprovisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: c10c313c5fc157ed70d2ccecfb930a8a765f8444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a>Tutorial: Integração do Azure Active Directory com SCC ciclo de vida
o objetivo deste tutorial Olá é integração de Olá tooshow do Azure e SCC ciclo de vida.  

cenário de Olá descrito neste tutorial pressupõe que já tenha Olá seguintes itens:

* Uma subscrição do Azure válida
* Um ciclo de vida SCC-início de sessão único (SSO) ativada subscrição

Depois de concluir este tutorial, Olá utilizadores do Azure AD que atribuiu tooSCC ciclo de vida será toosingle capaz de início de sessão na aplicação Olá no site da sua empresa SCC ciclo de vida (serviço fornecedor iniciada pelo início de sessão) ou utilizar Olá [introdução Painel de acesso de toohello](active-directory-saas-access-panel-introduction.md).

cenário de Olá descrito neste tutorial consiste em Olá blocos modulares os seguintes:

1. Ativar a integração de aplicações de Olá para SCC ciclo de vida
2. Configurar início de sessão único (SSO)
3. Configurar o aprovisionamento de utilizadores
4. Atribuir utilizadores

![Cenário](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "cenário")

## <a name="enable-hello-application-integration-for-scc-lifecycle"></a>Ativar a integração de aplicação Olá para SCC ciclo de vida
o objetivo desta secção Olá é toooutline como integração de aplicações de Olá tooenable para SCC ciclo de vida.

**integração de aplicações de Olá tooenable para ciclo de vida SCC, execute Olá os seguintes passos:**

1. No Olá portal clássico do Azure, no painel de navegação esquerdo Olá, clique em **do Active Directory**.
   
    ![Do Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "do Active Directory")
2. De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.
3. Clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.
   
    ![Aplicações](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "aplicações")
4. Clique em **adicionar** em Olá parte inferior da página Olá.
   
    ![Adicionar aplicação](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Adicionar aplicação")
5. No Olá **que itens pretende toodo** caixa de diálogo, clique em **adicionar uma aplicação na Galeria de Olá**.
   
    ![Adicionar uma aplicação de gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "adicionar uma aplicação de gallerry")
6. No Olá **caixa pesquisa**, tipo **SCC ciclo de vida**.
   
    ![Galeria de aplicações](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Galeria de aplicações")
7. No painel de resultados de Olá, selecione **SCC ciclo de vida**e, em seguida, clique em **concluída** aplicação de Olá tooadd.
   
    ![Ciclo de vida SCC](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC ciclo de vida")
   
## <a name="configure-single-sign-on"></a>Configurar o início de sessão único

o objetivo desta secção Olá é toooutline como tooenable utilizadores tooauthenticate tooSCC ciclo de vida à respetiva conta no Azure AD com Federação com base no protocolo SAML Olá.

**tooconfigure único início de sessão, execute Olá os seguintes passos:**

1. No Olá portal clássico do Azure, no Olá **SCC ciclo de vida** página de integração de aplicações, clique em **configurar o início de sessão único** tooopen Olá * * configurar início de sessão único * * caixa de diálogo.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "configurar o início de sessão único")
2. No Olá **como seria, como os utilizadores toosign no tooSCC ciclo de vida** página, selecione **Microsoft Azure AD Single Sign-On**e, em seguida, clique em **seguinte**.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "configurar o início de sessão único")
3. No Olá **URL da aplicação configurar** página, numa Olá **URL de início de sessão** caixa de texto, tipo Olá URL utilizado pelo seu toosign de utilizadores no tooyour aplicação SCC ciclo de vida utilizando Olá seguir o padrão "*https:// bs1.scc.com/lc7/Welcome/Customer/PICTtest.aspx*"e, em seguida, clique em **seguinte**.
   
    ![Configurar o URL da aplicação](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "configurar o URL da aplicação")
4. No Olá **configurar o início de sessão único no ciclo de vida SCC** página, clique em **transferir metadados**e, em seguida, guarde o ficheiro de metadados localmente no seu computador.
   
   ![Configurar o início de sessão único](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "configurar o início de sessão único")
5. Reencaminhe esse tooSCC de ficheiro de metadados equipa de suporte do ciclo de vida.
   
   >[!NOTE]
   >O início de sessão único tem toobe ativado por Olá SCC ciclo de vida a equipa de suporte.
   > 
   > 

6. No portal clássico do Azure Olá, selecione a confirmação de configuração de início de sessão único Olá e, em seguida, clique em **concluída** tooclose Olá **configurar início de sessão único** caixa de diálogo.
   
    ![Configurar o início de sessão único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "configurar o início de sessão único")
   
## <a name="configure-user-provisioning"></a>Configurar o aprovisionamento de utilizadores

Na ordem tooenable do Azure AD os utilizadores toolog no ciclo de vida SCC, têm de ser aprovisionados para SCC ciclo de vida. Não há nenhum item de ação para tooconfigure aprovisionamento de utilizadores tooSCC ciclo de vida.

Quando um toolog de tentativas de utilizador atribuído no ciclo de vida SCC, uma conta de ciclo de vida SCC é criada automaticamente se necessário.

>[!NOTE]
>Pode utilizar quaisquer outras SCC ciclo de vida utilizador conta criação ferramentas ou APIs fornecidas pelo SCC ciclo de vida tooprovision contas de utilizador do AAD.
> 
> 

## <a name="assign-users"></a>Atribuir utilizadores
tootest a configuração, terá de toogrant Olá do Azure AD utilizadores tooallow utilizando o tooit de acesso de aplicação atribuindo-los.

**tooassign utilizadores tooSCC ciclo de vida, execute Olá os seguintes passos:**

1. Olá portal clássico do Azure, crie uma conta de teste.
2. No Olá * * SCC ciclo de vida * * página de integração de aplicações, clique em **atribuir utilizadores**.
   
    ![Atribuir utilizadores](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "atribuir utilizadores")
3. Selecione o utilizador de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm a atribuição.
   
    ![Sim](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Sim")

Se quiser tootest as definições de SSO, abra Olá painel de acesso. Para obter mais detalhes sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).

