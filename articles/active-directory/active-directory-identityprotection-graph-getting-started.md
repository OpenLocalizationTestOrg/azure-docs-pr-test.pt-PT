---
title: aaaGet iniciado com o Azure Active Directory Identity Protection e o Microsoft Graph | Microsoft Docs
description: "Fornece uma introdução tooquery Microsoft Graph para obter uma lista de eventos de risco e informações associadas do Azure Active Directory."
services: active-directory
keywords: "eventos de risco, proteção de identidade do Azure Active Directory, a política de segurança, o Microsoft Graph e vulnerabilidade"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: fa109ba7-a914-437b-821d-2bd98e681386
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 75b8b7629a0120d8101f6fde0d9163122503d276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a>Introdução ao Azure Active Directory Identity Protection e o Microsoft Graph
Microsoft Graph é Olá Microsoft unified ponto final de API e Olá inicial de [do Azure Active Directory Identity Protection](active-directory-identityprotection.md) APIs. Olá primeira API, **identityRiskEvents**, permite-lhe tooquery Microsoft Graph para obter uma lista de [eventos de risco](active-directory-identityprotection-risk-events-types.md) e informações de associados. Este artigo obtém a começar a consultar esta API. Para uma introdução aprofundada, documentação completa e acesso toohello gráfico Explorer, consulte Olá [site Microsoft Graph](https://graph.microsoft.io/).

> [!IMPORTANT]
> A Microsoft recomenda que gere o Azure AD através de Olá [Centro de administração do Azure AD](https://aad.portal.azure.com) no Olá portal do Azure em vez de utilizar Olá portal clássico do Azure referenciado neste artigo.

Existem três passos tooaccessing identidade dados da proteção através do Microsoft Graph:

1. Adicione uma aplicação com um segredo do cliente. 
2. Utilize este segredo e alguns outros tipos de informações tooauthenticate tooMicrosoft gráfico, onde recebe um token de autenticação. 
3. Utilizar este ponto final do token toomake pedidos toohello API e voltar a dados da proteção de identidade.

Antes de começar, terá de:

* Aplicação da Olá de toocreate de privilégios de administrador no Azure AD
* nome de Olá de domínio do inquilino (por exemplo, contoso.onmicrosoft.com)

## <a name="add-an-application-with-a-client-secret"></a>Adicionar uma aplicação com um segredo do cliente
1. [Inicie sessão no](https://manage.windowsazure.com) tooyour portal clássico do Azure como administrador. 
2. No painel de navegação esquerdo Olá, clique em **do Active Directory**. 
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.
4. No menu de Olá na parte superior do Olá, clique em **aplicações**.
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. Clique em **adicionar** em Olá parte inferior da página Olá.
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. No Olá **que itens pretende toodo** caixa de diálogo, clique em **adicionar uma aplicação que a minha organização está a desenvolver**.
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. No Olá **conte-na sua aplicação** caixa de diálogo, efetuar Olá os seguintes passos:
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    a. No Olá **nome** caixa de texto, escreva um nome para a sua aplicação (por ex.: aplicação de API de eventos de risco AADIP).
   
    b. Como **tipo**, selecione **aplicação Web e / ou Web API**.
   
    c. Clique em **Seguinte**.
8. No Olá **as propriedades da aplicação** caixa de diálogo, efetuar Olá os seguintes passos:
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    a. No Olá **URL de início de sessão** caixa de texto, tipo `http://localhost`.
   
    b. No Olá **URI de ID de aplicação** caixa de texto, tipo `http://localhost`.
   
    c. Clique em **Concluído**.

Agora pode configurar a sua aplicação.

![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-toouse-hello-api"></a>Conceder a Olá de toouse de permissão de aplicação API
1. Na página da aplicação, no menu de Olá na parte superior do Olá, clique em **configurar**. 
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. No Olá **aplicações de tooother permissões** secção, clique em **Adicionar aplicação**.
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. No Olá **aplicações de tooother permissões** caixa de diálogo, efetuar Olá os seguintes passos:
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    a. Selecione **Microsoft Graph**.
   
    b. Clique em **Concluído**.
4. Clique em **permissões de aplicação: 0**e, em seguida, selecione **ler todas as informações de eventos de risco de identidade**.
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. Clique em **guardar** em Olá parte inferior da página Olá.
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a>Obter uma chave de acesso
1. Na página da aplicação, na Olá **chaves** secção, selecione de 1 ano como duração.
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. Clique em **guardar** em Olá parte inferior da página Olá.
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. na secção de chaves de Olá, copie o valor de Olá da sua chave recentemente criada e, em seguida, cole-o numa localização segura.
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > Se perder a esta chave, irá ter tooreturn toothis secção e crie uma nova chave. Manter esta chave de segredo: qualquer pessoa que tenha pode aceder aos seus dados.
   > 
   > 
4. No Olá **propriedades** secção, Olá cópia **ID de cliente**e, em seguida, cole-o numa localização segura. 

## <a name="authenticate-toomicrosoft-graph-and-query-hello-identity-risk-events-api"></a>Autenticar tooMicrosoft gráfico e Olá de consulta API de eventos de risco de identidade
Neste momento, é necessário:

* ID de cliente Olá copiou acima
* chave de Olá que copiou acima
* nome de Olá do domínio do seu inquilino

tooauthenticate, envie uma mensagem de pedido demasiado`https://login.microsoft.com` com Olá seguir os parâmetros no corpo de Olá:

* grant_type: "**client_credentials**"
* recurso: "**https://graph.microsoft.com**"
* client_id:<your client ID>
* client_secret:<your key>

> [!NOTE]
> Precisa de valores de tooprovide para Olá **client_id** e Olá **client_secret** parâmetro.
> 
> 

Se tiver êxito, esta ação devolve um token de autenticação.  
Olá toocall API, criar um cabeçalho com Olá seguinte parâmetro:

    `Authorization`=”<token_type> <access_token>"


Quando a autenticação, pode encontrar o tipo de token de Olá e o token de acesso no Olá devolvida um token.

Envie este cabeçalho como um toohello pedido seguinte URL de API:`https://graph.microsoft.com/beta/identityRiskEvents`

resposta de Olá, se tiver êxito, é uma coleção de identidade eventos de risco e dados no formato JSON de OData, que pode ser analisado e processado como julgar de Olá associados.

Eis o código de exemplo para autenticar e chamar a API de Olá através do Powershell.  
Basta adicionar o seu ID de cliente, a chave e domínio de inquilino.

    $ClientID       = "<your client ID here>"        # Should be a ~36 hex character string; insert your info here
    $ClientSecret   = "<your client secret here>"    # Should be a ~44 character string; insert your info here
    $tenantdomain   = "<your tenant domain here>"    # For example, contoso.onmicrosoft.com

    $loginURL       = "https://login.microsoft.com"
    $resource       = "https://graph.microsoft.com"

    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    Write-Output $oauth

    if ($oauth.access_token -ne $null) {
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

        $url = "https://graph.microsoft.com/beta/identityRiskEvents"
        Write-Output $url

        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)

        foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
            Write-Output $event
        }

    } else {
        Write-Host "ERROR: No Access Token"
    } 


## <a name="next-steps"></a>Passos seguintes
Parabéns, efetuadas apenas o primeiro tooMicrosoft de chamada gráfico!  
Agora pode consultar eventos de risco de identidade e utilizar dados Olá, no entanto, julgar.

toolearn mais informações sobre o Microsoft Graph e como aplicações toobuild utilizando Olá Graph API, consulte Olá [documentação](https://graph.microsoft.io/docs) e muito mais no Olá [site Microsoft Graph](https://graph.microsoft.io/). Além disso, certifique-se de que toobookmark Olá [API do Azure AD Identity Protection](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) página que lista todos os Olá APIs de proteção de identidade disponíveis no gráfico. À medida que adiciona novas formas toowork com proteção de identidade através de API, irá vê-los nessa página.

## <a name="additional-resources"></a>Recursos adicionais
* [Proteção de identidade do Azure Active Directory](active-directory-identityprotection.md)
* [Tipos de eventos de risco detetados pelo Azure Active Directory Identity Protection](active-directory-identityprotection-risk-events-types.md)
* [Microsoft Graph](https://graph.microsoft.io/)
* [Descrição geral do Microsoft Graph](https://graph.microsoft.io/docs)
* [Raiz do serviço do Azure AD Identity Protection](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

