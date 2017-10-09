---
title: "aaaConfigure autenticação e autorização para uma aplicação personalizada que chama Olá Azure tempo série Insights API | Microsoft Docs"
description: "Este tutorial explica como tooconfigure autenticação e autorização para uma aplicação personalizada que chama Olá API de Insights de série de tempo do Azure"
keywords: 
services: time-series-insights
documentationcenter: 
author: dmdenmsft
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/24/2017
ms.author: dmden
ms.openlocfilehash: 5043468bfc2af3c0d27e8602508d92ba2848409e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a>Autenticação e autorização para API de Insights de série de tempo do Azure

Este artigo explica como tooconfigure uma aplicação personalizada que chama Olá API de Insights de série de tempo do Azure.

## <a name="service-principal"></a>Principal de serviço

Esta secção explica como tooconfigure tooaccess uma aplicação Olá tempo série Insights API em nome da aplicação Olá. aplicação Olá, em seguida, pode consultar dados ou publicar dados de referência no ambiente de informações de séries de tempo de Olá com credenciais de aplicação e credenciais de utilizador não Olá.

Quando tiver uma aplicação que necessita de tooaccess Insights de séries de tempo, tem de configurar uma aplicação do Azure Active Directory e atribuir políticas de acesso de dados Olá no ambiente do Olá Insights de séries de tempo. Esta abordagem é preferível toorunning Olá aplicação com as suas próprias credenciais porque:

* Pode atribuir permissões de identidade de aplicação toohello que são diferentes das suas permissões. Normalmente, estas permissões são tooexactly restrito tem de aplicação que Olá toodo. Por exemplo, pode permitir Olá aplicação tooonly ler os dados num ambiente Insights de séries de tempo específico.
* Não tem credenciais da aplicação Olá toochange se alterar as suas responsabilidades.
* Pode utilizar um certificado ou uma autenticação de chave tooautomate aplicação quando estiver a executar um script automático.

Este artigo mostra como tooperform os passos através de Olá portal do Azure. Concentra-se uma aplicação do inquilino único em que a aplicação Olá é toorun pretendido na organização apenas um. Normalmente utiliza aplicações de inquilino único para aplicações de linha de negócio que são executadas na sua organização.

fluxo de configuração de Olá consiste em três passos de alto nível:

1. Crie uma aplicação no Azure Active Directory.
2. Autorize o ambiente do Insights de séries de tempo tooaccess Olá esta aplicação.
3. Utilizar o ID da aplicação Olá e chave tooacquire um token toohello `"https://api.timeseries.azure.com/"` audiência ou recurso. token de Olá, em seguida, pode ser utilizados toocall Olá API de informações de séries de tempo.

Eis os passos detalhados de hello:

1. No portal do Azure Olá, selecione **do Azure Active Directory** > **registos de aplicação** > **novo registo de aplicação**.

   ![Novo registo de aplicação no Azure Active Directory](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. Dar um toobe de tipo Olá nome, selecione a aplicação Olá **aplicação Web / API**, selecione qualquer URI válido para **URL de início de sessão**e clique em **criar**.

   ![Criar aplicação Olá no Azure Active Directory](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. Selecione a aplicação criada recentemente e copie o editor de texto favorito de tooyour de ID de aplicação.

   ![Copie o ID da aplicação Olá](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. Selecione **chaves**, introduza o nome da chave Olá, expiração selecione Olá e clique em **guardar**.

   ![Selecione as chaves de aplicação](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Introduza o nome da chave Olá e expiração e clique em Guardar](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. Copie o editor de texto favorito Olá tooyour chave.

   ![Copie a chave da aplicação Olá](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. Para o ambiente de informações de séries de tempo de Olá, selecione **políticas de acesso de dados** e clique em **adicionar**.

   ![Adicionar novo dados acesso política toohello Insights de séries de tempo ambiente](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. No Olá **selecionar utilizador** caixa de diálogo, o nome da aplicação Olá Colar (a partir do passo 2) ou o ID da aplicação (a partir do passo 3).

   ![Localizar uma aplicação na caixa de diálogo Selecionar utilizador Olá](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. Função de Olá selecione (**leitor** para consultar os dados, **contribuinte** para consultar os dados e a alteração de dados de referência) e clique em **Ok**.

   ![Escolher o leitor ou contribuinte na caixa de diálogo Selecionar função Olá](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. Guardar política de Olá clicando **Ok**.

10. Utilize o ID da aplicação Olá (a partir do passo 3) e chave (a partir do passo 5) tooacquire Olá o token de aplicações em nome da aplicação Olá. Olá token pode, em seguida, ser transmitido no Olá `Authorization` cabeçalho quando chamadas de aplicação Olá Olá API de informações de séries de tempo.

    Se estiver a utilizar c#, pode utilizar Olá token de Olá tooacquire código em nome da aplicação Olá a seguir. Para um exemplo completo, consulte [consultar dados com c#](time-series-insights-query-data-csharp.md).

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set hello resource URI toohello Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of hello application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a>Passos seguintes

Utilizar o ID da aplicação Olá e chave na sua aplicação. Para o código de exemplo que chama a API de informações de séries de tempo de Olá, consulte [consultar dados com c#](time-series-insights-query-data-csharp.md).

## <a name="see-also"></a>Consultar também

* [API de consulta](/rest/api/time-series-insights/time-series-insights-reference-queryapi) para referência da API de consulta completa Olá
* [Criar um serviço principal no Olá portal do Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md)
