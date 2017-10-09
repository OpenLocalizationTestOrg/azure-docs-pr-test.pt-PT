---
title: "API de relatórios aaaPrerequisites tooaccess Olá do Azure AD | Microsoft Docs"
description: "Saiba mais sobre API relatórios do Olá pré-requisitos tooaccess Olá do Azure AD"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ec28a7530f341dda31268a978754b615c727d66f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a>API de relatórios pré-requisitos tooaccess Olá do Azure AD

Olá [relatório APIs do Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) lhe fornecer os dados de toohello acesso programático através de um conjunto de APIs baseado em REST. Pode chamar estas APIs a partir de várias linguagens e ferramentas de programação.

Olá reporting utiliza API [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) as APIs do web toohello tooauthorize acesso. 

tooget aceder aos dados de relatórios toohello através da API de Olá, precisa toohave uma Olá funções atribuídas a seguir:

- Leitor de segurança
- Administrador de segurança
- Administrador global


tooprepare sua toohello acesso API do relatório, tem de:

1. Registar uma aplicação 
2. Conceder permissões 
3. Recolher as definições de configuração 

Para perguntas, problemas ou comentários, consulte [um pedido de suporte de ficheiros](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).

## <a name="register-an-azure-active-directory-application"></a>Registar uma aplicação do Azure Active Directory

É necessário tooregister uma aplicação, mesmo que se estão a aceder Olá API através de um script do relatório. Isto dá-lhe um **ID da aplicação**, que é necessário para uma chamada de autorização e permite que os tokens de tooreceive de código.

tooconfigure diretório tooaccess Olá do Azure AD relatórios API, tem de iniciar sessão toohello portal do Azure com uma conta de administrador do Azure que também seja membro de Olá **Administrador Global** função de diretório no seu inquilino do Azure AD .

> [!IMPORTANT]
> As aplicações em execução sob credenciais com privilégios de "admin" como este podem ser muito poderosas, por isso, tenha ser as credenciais de ID/segredo da aplicação do se tookeep Olá segura.
> 


**tooregister uma aplicação do Azure Active Directory:**

1. No Olá [portal do Azure](https://portal.azure.com), no painel de navegação esquerdo de Olá, clique em **do Active Directory**.
   
    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. No Olá **do Azure Active Directory** painel, clique em **registos de aplicação**.

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. No Olá **registos de aplicação** painel, na barra de ferramentas de Olá na parte superior do Olá, clique em **novo registo de aplicação**.

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. No Olá **criar** painel, efetuar Olá os seguintes passos:

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    a. No Olá **nome** caixa de texto, tipo `Reporting API application`.

    b. Como **tipo de aplicação**, selecione **aplicação Web / API**.

    c. No Olá **URL de início de sessão** caixa de texto, tipo `https://localhost`.

    d. Clique em **Criar**. 


## <a name="grant-permissions"></a>Conceder permissões 

o objetivo deste passo Olá é toogrant a aplicação **ler os dados de diretório** permissões toohello **Windows Azure Active Directory** API.

![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

**toogrant Olá de toouse permissão da aplicação API:**

1. No Olá **registos de aplicação** painel, na lista de aplicações de Olá, clique em **aplicação API de relatórios**.

2. No Olá **aplicação API de relatórios** painel, na barra de ferramentas de Olá na parte superior do Olá, clique em **definições**. 

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. No Olá **definições** painel, clique em **as permissões necessárias**. 

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. No Olá **as permissões necessárias** painel, no Olá **API** lista, clique em **Windows Azure Active Directory**. 

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. No Olá **ativar o acesso ao** painel, selecione **ler os dados de diretório**. 

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. Na barra de ferramentas Olá na parte superior do Olá, clique em **guardar**.

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a>Recolher as definições de configuração 
Esta secção mostra-lhe como Olá tooget seguintes definições de diretório:

* Nome de domínio
* ID de cliente
* Segredo do cliente

Necessitar destes valores quando configurar a API de relatórios de toohello de chamadas. 

### <a name="get-your-domain-name"></a>Obter o nome de domínio

**tooget seu nome de domínio:**

1. No Olá [portal do Azure](https://portal.azure.com), no painel de navegação esquerdo de Olá, clique em **do Active Directory**.
   
    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. No Olá **do Azure Active Directory** painel, clique em **nomes de domínio**.

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. Copie o seu nome de domínio na lista de Olá de domínios.


### <a name="get-your-applications-client-id"></a>Obter ID de cliente da aplicação

**tooget ID de cliente da aplicação:**

1. No Olá [portal do Azure](https://portal.azure.com), no painel de navegação esquerdo de Olá, clique em **do Active Directory**.
   
    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. No Olá **registos de aplicação** painel, na lista de aplicações de Olá, clique em **aplicação API de relatórios**.

3. No Olá **aplicação API de relatórios** painel, em Olá **ID da aplicação**, clique em **clique toocopy**.

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a>Obter o segredo do cliente da aplicação
tooget cliente da sua aplicação secreta, que precisa toocreate uma nova chave e guarde respectivo valor após guardar a nova chave de Olá porque não é possível tooretrieve este valor já mais tarde.

**tooget segredo do cliente da aplicação:**

1. No Olá [portal do Azure](https://portal.azure.com), no painel de navegação esquerdo de Olá, clique em **do Active Directory**.
   
    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. No Olá **registos de aplicação** painel, na lista de aplicações de Olá, clique em **aplicação API de relatórios**.


3. No Olá **aplicação API de relatórios** painel, na barra de ferramentas de Olá na parte superior do Olá, clique em **definições**. 

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. No Olá **definições** painel, no Olá **APIR acesso** secção, clique em **chaves**. 

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. No Olá **chaves** painel, efetuar Olá os seguintes passos:

    ![Registar a aplicação](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    a. No Olá **Descrição** caixa de texto, tipo `Reporting API`.

    b. Como **expira**, selecione **nos 2 anos**.

    c. Clique em **Guardar**.

    d. Copie o valor da chave Olá.


## <a name="next-steps"></a>Passos Seguintes
* Seria que como tooaccess Olá dados a partir do Azure AD de Olá API do relatório de forma programática? Veja [introdução Olá API do Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md).
* Se quiser toofind mais informações sobre os relatórios do Azure Active Directory, consulte Olá [do Azure Active Directory guia de relatórios](active-directory-reporting-guide.md).  

